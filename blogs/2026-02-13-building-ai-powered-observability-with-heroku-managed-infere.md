---
title: "Building AI-Powered Observability with Heroku Managed Inference and Agents"
url: "https://www.heroku.com/blog/building-ai-powered-observability-with-managed-inference-and-agents/"
date: "Fri, 13 Feb 2026 19:36:30 +0000"
author: "Karunasri (Karuna) Garigipati"
feed_url: "https://www.heroku.com/feed/"
---
<p>If you&#8217;ve ever debugged a production incident, you know the drill: IDE on one screen, Splunk on another, Sentry open in a third tab, frantically copying error messages between windows while your PagerDuty keeps buzzing.</p>
<p>You ask &#8220;What errors spiked in the last hour?&#8221; but instead of an answer, you have to context-switch, recall complex query syntax, and mentally correlate log timestamps with your code. By the time you find the relevant log, you&#8217;ve lost your flow. Meanwhile the incident clock keeps ticking away.</p>
<p>The workflow below fixes that broken loop. We’ll show you how to use the <a href="https://www.heroku.com/ai/mcp-on-heroku/">Model Context Protocol (MCP)</a> and <a href="https://www.heroku.com/ai/managed-inference-and-agents/">Heroku Managed Inference and Agents</a> to pipe those observability queries directly into your IDE, turning manual hunting into instant answers.</p>
<p><span id="more-18630"></span></p>
<h2>Connecting telemetry to code for AI-powered observability</h2>
<p>The system connects AI coding assistants to observability platforms through the Model Context Protocol (MCP), with Managed Inference and Agents handling the transport layer.</p>
<figure class="wp-caption alignnone" id="attachment_18633" style="width: 2683px;"><img alt="A flowchart shows a developer using an AI assistant to call a Splunk tool, with requests and responses passing through Heroku Managed Inference, MCP servers, and resulting JSON output." class="wp-image-18633 size-full" height="1162" src="https://www.heroku.com/wp-content/uploads/2026/02/heroku-mcp-sequence-diagram.png" width="2683" /><figcaption class="wp-caption-text" id="caption-attachment-18633">What we built for AI-powered observability with Heroku Managed Inference and Agents</figcaption></figure>
<h3>Building the MCP servers</h3>
<h4>Unified tool interface</h4>
<p>We expose each observability platform through MCP&#8217;s consistent tool interface. Here&#8217;s how we define a Splunk search tool:</p>
<pre class="language-go"><code>searchTool := mcp.NewTool("search_splunk",
    mcp.WithDescription("Execute a Splunk search query and return the results."),
    mcp.WithString("search_query", mcp.Description("The search query to execute")),
    mcp.WithString("earliest_time", mcp.Description("Start time for the search")),
    mcp.WithString("latest_time", mcp.Description("End time for the search")),
    mcp.WithNumber("max_results", mcp.Description("Maximum number of results")),
)
</code></pre>
<p>The AI assistant sees this as a callable tool with typed parameters. When a user asks about errors, the assistant decides which tool to call and constructs the appropriate arguments.</p>
<h4>Handling tool calls</h4>
<p>Tool handlers translate MCP requests into platform-specific API calls:</p>
<pre class="language-go"><code>s.AddTool(searchTool, func(ctx context.Context, request mcp.CallToolRequest) (*mcp.CallToolResult, error) {
    searchQuery, _ := request.RequireString("search_query")
    earliestTime := request.GetString("earliest_time", "-24h")
    latestTime := request.GetString("latest_time", "now")
    maxResults := request.GetInt("max_results", 100)

    results, err := client.Search(ctx, searchQuery, earliestTime, latestTime, maxResults)
    if err != nil {
        return mcp.NewToolResultText(fmt.Sprintf("Error: %v", err)), nil
    }

    resultData, _ := json.Marshal(results)
    return mcp.NewToolResultText(string(resultData)), nil
})
</code></pre>
<h2>Multi-platform support</h2>
<p>The same pattern works across observability platforms. For Honeycomb, we expose dataset queries with filters and breakdowns:</p>
<pre class="language-go"><code>queryTool := mcp.NewTool("query_honeycomb",
    mcp.WithDescription("Execute a Honeycomb query with filters and breakdowns"),
    mcp.WithString("dataset", mcp.Description("The dataset to query")),
    mcp.WithString("calculation", mcp.Description("COUNT, AVG, P99, etc.")),
    mcp.WithString("filter_column", mcp.Description("Column to filter on")),
    mcp.WithString("filter_value", mcp.Description("Value to filter for")),
)
</code></pre>
<p>For Sentry, in addition to Sentry tools, we enabled direct event lookup from URLs—paste a Sentry link and get the full JSON:</p>
<pre class="language-go"><code>eventTool := mcp.NewTool("get_sentry_event",
    mcp.WithDescription("Get event by URL or ID - paste Sentry event URL to fetch full JSON"),
    mcp.WithString("event_url_or_id", mcp.Description("Sentry event URL or event ID")),
)
</code></pre>
<h2>Deploying with Heroku Managed Inference and Agents</h2>
<p>Heroku Managed Inference and Agents provides an MCP gateway that handles the SSE transport layer, letting you deploy MCP servers as simple STDIO processes.</p>
<p>Create app, attach Add-on, configure, and deploy:</p>
<pre class="language-bash"><code>heroku create your-observability-mcp
heroku addons:create heroku-inference:claude-4-5-haiku -a your-observability-mcp
# Set credentials for your observability platform
heroku config:set YOUR_PLATFORM_CREDENTIALS -a your-observability-mcp
# Deploy
git push heroku main
</code></pre>
<p>Get the inference token:</p>
<pre class="language-bash"><code>heroku config:get INFERENCE_KEY -a your-observability-mcp</code></pre>
<p>Team members add this to their Cursor or Claude configuration:</p>
<pre class="language-json"><code>{
  "mcpServers": {
    "splunk": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://us.inference.heroku.com/mcp/sse",
               "--header", "Authorization:Bearer YOUR_INFERENCE_TOKEN"]
    }
  }
}
</code></pre>
<p><img alt="A list of three installed MCP servers: heroku-honeycomb with 6 tools, heroku-sentry with 8 tools, and heroku-splunk with 5 tools, all toggled on." class="alignnone wp-image-18632 size-full" height="456" src="https://www.heroku.com/wp-content/uploads/2026/02/mcp-servers.png" width="1140" /></p>
<h3>Contextualizing error spikes</h3>
<p>In a traditional dashboard, you see a red bar. With MCP, you get an answer. We asked the agent, <em>&#8220;What error types are most common in production today?&#8221;</em> and it returned the ranked list below.</p>
<table style="width: 100%; margin-bottom: 30px;">
<thead>
<tr>
<th>Rank</th>
<th>Error Type</th>
<th>Count</th>
<th>Primary Source</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>TimeoutException</td>
<td>847</td>
<td>checkout-service, payment processing</td>
</tr>
<tr>
<td>2</td>
<td>ConnectionRefused</td>
<td>312</td>
<td>database pool exhaustion, redis</td>
</tr>
<tr>
<td>3</td>
<td>NullPointerException</td>
<td>156</td>
<td>user-profile-api, missing field handling</td>
</tr>
<tr>
<td>4</td>
<td>RateLimitExceeded</td>
<td>98</td>
<td>external-api-gateway, third-party calls</td>
</tr>
<tr>
<td>5</td>
<td>AuthenticationFailed</td>
<td>67</td>
<td>session-service, expired tokens</td>
</tr>
<tr>
<td>6</td>
<td>ResourceNotFound</td>
<td>54</td>
<td>inventory-api, stale cache references</td>
</tr>
<tr>
<td>7</td>
<td>CircuitBreakerOpen</td>
<td>41</td>
<td>payments-api, downstream failures</td>
</tr>
<tr>
<td>8</td>
<td>DeserializationError</td>
<td>28</td>
<td>webhook-processor, malformed payloads</td>
</tr>
</tbody>
</table>
<p>While the distribution might look standard, the AI can help you interpret the security implications. For example, the AI can correlate a rise in <code>AuthenticationFailed</code> errors with specific geographic regions to confirm a brute-force attempt or credential attack, or identify that <code>RateLimitExceeded</code> errors are coming from a single subnet. This context transforms a generic &#8220;error count&#8221; into actionable security intelligence.</p>
<h2>Why AI-native observability changes the game</h2>
<p>Connecting your observability stack to your IDE via MCP does more than just save you a few clicks; it keeps you in the flow during an incident. By letting Heroku Managed Inference and Agents handle the proprietary query syntax, any engineer can interrogate production data as easily as a platform specialist. Why this works better:</p>
<ul>
<li><strong>Automate complex security audits</strong>: We processed 175,000+ events in minutes to clear a suspicious account flag, turning hours of manual log analysis into a single natural language question.</li>
<li><strong>Bypass the syntax barrier</strong>: Engineers ask questions in natural language instead of wrestling with complex SPL or Honeycomb queries. No one needs to remember platform-specific syntax at 2 AM.</li>
<li><strong>Deploy &#8220;Day One&#8221; observability</strong>: New hires can query production state immediately without mastering your specific observability stack or acronyms. The AI translates intent into execution.</li>
<li><strong>Debug directly in context</strong>: Stop toggling between IDE and browser. By pulling telemetry into your local environment, you keep your mental model intact and fix issues where the code lives..</li>
<li><strong>Instant root cause analysis</strong>: Simply paste a URL to get an immediate root cause analysis with suggested fixes, skipping the manual correlation step entirely.</li>
</ul>
<h2>Extend your AI assistant with any API</h2>
<p>Moving from siloed observability tools to an AI-integrated debugging workflow requires bridging the gap between platforms and your IDE. We built this using Heroku Managed Inference and Agents and the Model Context Protocol, and the same pattern works for any API you want to bring into your AI assistant.</p>
<p>Whether it&#8217;s observability, internal tools, or customer data — if you can call an API, you can expose it as an MCP tool. Heroku Managed Inference and Agents handles the transport, authentication, and hosting. You focus on the integration.</p>
<p>What will you build? <a class="cta-link elementor-button-link" href="https://elements.heroku.com/addons/heroku-inference">Get started with Heroku Managed Inference and Agents</a></p>
<p>The post <a href="https://www.heroku.com/blog/building-ai-powered-observability-with-managed-inference-and-agents/">Building AI-Powered Observability with Heroku Managed Inference and Agents</a> appeared first on <a href="https://www.heroku.com">Heroku</a>.</p>
