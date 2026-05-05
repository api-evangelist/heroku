---
title: "Code Execution Sandbox for Agents on Heroku"
url: "https://www.heroku.com/blog/code-execution-sandbox-for-agents-on-heroku/"
date: "Tue, 17 Feb 2026 20:34:33 +0000"
author: "Anush DSouza"
feed_url: "https://www.heroku.com/feed/"
---
<p>Large language models are good at writing code. Data from Anthropic shows that allowing Claude to execute scripts, rather than relying on sequential tool calls, reduces token consumption by an average of 37%, with some use cases seeing reductions as high as 98%.</p>
<p>Untrusted code needs a secure and isolated place to execute. We solved this with <a href="https://github.com/heroku/mcp-code-exec-python">code execution sandboxes</a> (powered by <a href="https://devcenter.heroku.com/articles/one-off-dynos">one-off dynos</a>), launched alongside <a href="https://elements.heroku.com/addons/heroku-inference">Heroku Managed Inference and Agents</a> in May 2025.</p>
<p><span id="more-18656"></span></p>
<p>You can leverage these sandboxes in two ways:</p>
<ul>
<li><strong>Built-in tools</strong>, within our <a href="https://devcenter.heroku.com/articles/heroku-inference-api-v1-agents-heroku">Managed Inference and Agents API</a></li>
<li><strong>MCP tool</strong>, by deploying our open-source Model Context Protocol (MCP) servers to connect the sandbox to any client, including Agentforce, Claude Desktop, or Cursor</li>
</ul>
<h2>How agents improve with code execution tools</h2>
<p>Every tool definition and intermediate output is forced through the model&#8217;s context window. This is highly inefficient. For example, if you analyze a 10MB log file, the entire file consumes your context even if you only need a brief summary of the errors.</p>
<p>The better pattern, which Anthropic calls <a href="https://platform.claude.com/docs/en/agents-and-tools/tool-use/programmatic-tool-calling">programmatic tool calling</a>, lets the model write code that orchestrates everything.</p>
<p>If you’re using Salesforce and want to ask Agentforce to find at-risk deals in your Q1 pipeline, the agent writes a script that queries thousands of opportunities, cross-references activity history, filters for deals with no recent engagement, and returns just the 12 that need attention. The tool execution and reasoning and analysis can happen in the Heroku sandbox and only the summary hits the model&#8217;s context.</p>
<h2>Isolation via one-off dynos</h2>
<p>To execute untrusted code safely, we use <a href="https://devcenter.heroku.com/articles/one-off-dynos">one-off dynos</a>. This is the same infrastructure that has been used for administrative or maintenance tasks on Heroku for over a decade. Because these dynos are spun up on demand and terminate after use, they provide a naturally isolated, cost-effective, and secure environment, which means the blast radius of LLM generated code is limited to an ephemeral container.</p>
<h2>How to use the built-in tools</h2>
<p>If you&#8217;re using the <a href="https://devcenter.heroku.com/articles/heroku-inference-api-v1-agents-heroku">Managed Inference and Agents API</a>, include <a href="https://github.com/heroku/mcp-code-exec-python">code_exec_python</a> (or <a href="https://github.com/heroku/mcp-code-exec-ruby">code_exec_ruby</a>, <a href="https://github.com/heroku/mcp-code-exec-node">code_exec_node</a>, <a href="https://github.com/heroku/mcp-code-exec-go">code_exec_go</a>) in your tool list:</p>
<pre class="language-bash"><code>curl "$INFERENCE\_URL/v1/agents/heroku" \\
  -H "Content-Type: application/json" \\
  -H "Authorization: Bearer $INFERENCE\_KEY" \\
  -d '{
    "model": "claude-4-sonnet",
    "messages": [
      {
        "role": "user",
        "content": "Calculate the standard deviation of [23, 45, 67, 12, 89, 34, 56, 78, 90, 11]"
      }
    ],
    "tools": [
      {
        "type": "heroku_tool",
        "name": "code_exec_python"
      }
    ]
  }'
</code></pre>
<p>The agent writes Python, we execute it in a dyno, and stream back the result:</p>
<pre class="language-bash"><code>{  
  "choices": [  
    {  
      "message": {  
        "role": "assistant",  
        "content": "The standard deviation is 30.19. Here's what I calculated:\n\nMean: 50.5\nVariance: 911.39\nStd Dev: 30.19\n\nThe data has fairly high spread - values range from 11 to 90."  
      }  
    }  
  ]  
}
</code></pre>
<p>You can pass <code>runtime_params</code> with <code>max_calls</code> to limit how many times the tool runs during a single agent loop.</p>
<h2>Deploying your own code execution MCP server</h2>
<p>For Agentforce, Claude Desktop, Cursor, or custom frameworks, deploy the MCP server directly:</p>
<pre class="language-bash"><code>git clone https://github.com/heroku/mcp-code-exec-python
cd mcp-code-exec-python
heroku create my-sandbox
heroku config:set API_KEY=$(openssl rand -hex 32)
git push heroku main
</code></pre>
<p>The server implements the Model Context Protocol. Point your client at it and you get the same sandboxed execution. We have implementations for <a href="https://github.com/heroku/mcp-code-exec-python">Python</a>, <a href="https://github.com/heroku/mcp-code-exec-ruby">Ruby</a>, <a href="https://github.com/heroku/mcp-code-exec-node">Node</a>, and <a href="https://github.com/heroku/mcp-code-exec-go">Go</a>. Each repo has a deploy button if you prefer one-click setup.</p>
<p>Start building more powerful, efficient AI agents by <a href="https://devcenter.heroku.com/articles/heroku-inference-tools#heroku-tool-code_exec_">trying out our code execution sandboxes</a> today.</p>
<p>The post <a href="https://www.heroku.com/blog/code-execution-sandbox-for-agents-on-heroku/">Code Execution Sandbox for Agents on Heroku</a> appeared first on <a href="https://www.heroku.com">Heroku</a>.</p>
