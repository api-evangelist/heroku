---
title: "Whats New in Heroku AI: New Models and a Flexible Standard Plan"
url: "https://www.heroku.com/blog/new-models-and-flexible-standard-plan/"
date: "Thu, 19 Feb 2026 17:08:20 +0000"
author: "Anush DSouza"
feed_url: "https://www.heroku.com/feed/"
---
<p>Heroku is introducing significant updates to <a href="https://elements.heroku.com/addons/heroku-inference">Managed Inference and Agents</a>. These changes focus on reducing developer friction, expanding model catalogue, and streamlining deployment workflows.<br />
<span id="more-18661"></span></p>
<h2>More flexibility with the new standard plan</h2>
<p>Until now, Heroku’s model-based plans required developers to provision a specific add-on for a specific model. This created significant operational overhead. If you wanted to experiment with a different model or implement a fallback strategy, you had to provision a new add-on and manage multiple config variables.</p>
<p>We have added a new <a href="https://elements.heroku.com/addons/heroku-inference#tab-standard">standard plan</a> for <a href="https://elements.heroku.com/addons/heroku-inference">Heroku Managed Inference and Agents</a>.</p>
<p>With this update, a single add-on and a single API key grant access to our entire catalog of supported models. You no longer need to reprovision resources to switch from a smaller model to a high-reasoning model. Instead, you simply update the model name in your code. This unified approach improves developer experience and allows for more robust application architectures. Try the standard mode using the following CLI command:</p>
<pre class="language-bash"><code>$ heroku addons:create heroku-inference:standard -a $APPNAME
</code></pre>
<h2>New frontier models and an expanded open-weight catalog</h2>
<h3>Claude 4.6 models</h3>
<p>Heroku now supports the Claude 4.6 family, the most capable models in the Claude family, designed for high-complexity workloads.</p>
<ul>
<li><a href="https://devcenter.heroku.com/articles/heroku-inference-api-model-claude-opus-4-6"><strong>Claude Opus 4.6</strong></a>: Designed for advanced software development, complex agentic workflows, and long-horizon planning.</li>
<li><a href="https://devcenter.heroku.com/articles/heroku-inference-api-model-claude-sonnet-4-6"><strong>Claude Sonnet 4.6</strong></a>: High-performing model that is ideal as a daily driver and sophisticated financial analysis.</li>
</ul>
<h3>Open-weight models</h3>
<p>We have also expanded our catalog with five new open-weight models to provide more cost-effective options for diverse use cases.</p>
<ul>
<li><a href="https://devcenter.heroku.com/articles/heroku-inference-api-model-deepseek-v3-2"><strong>DeepSeek v3.2</strong></a>: Advanced model built for high-efficiency agentic reasoning and long-context understanding.</li>
<li><a href="https://devcenter.heroku.com/articles/heroku-inference-api-model-kimi-k2-5"><strong>Kimi K2.5</strong></a>: Optimized for massive context processing, advanced mathematical reasoning, and complex agent swarms.</li>
<li><a href="https://devcenter.heroku.com/articles/heroku-inference-api-model-minimax-m2-1"><strong>MiniMax M2.1</strong></a>: Specialized for practical engineering and multi-language full-stack application building.</li>
<li><a href="https://devcenter.heroku.com/articles/heroku-inference-api-model-glm-4-7"><strong>ZAI GLM 4.7</strong></a>: Industry-leading model for reliable tool-calling and vibe coding visually aesthetic front-ends.</li>
<li><a href="https://devcenter.heroku.com/articles/heroku-inference-api-model-glm-4-7-flash"><strong>ZAI GLM 4.7 Flash</strong></a>: A lightweight model optimized for speed, cost-efficiency, and agentic workflows where responsiveness is critical.</li>
</ul>
<h3>Embed models</h3>
<p>We are enhancing our support for vector-based search and retrieval with a new Cohere Embed V4 model. The latest generation of Cohere&#8217;s embedding technology is built for higher accuracy and complex document analysis.</p>
<ul>
<li><a href="https://devcenter.heroku.com/articles/heroku-inference-api-model-cohere-embed-v4"><strong>Cohere Embed V4</strong></a>: Specifically designed to understand conceptual relationships rather than just keyword matching.</li>
</ul>
<h3>Model deprecation notice</h3>
<p>As we transition to these next-generation models, we are beginning the deprecation process for older versions, including Claude 3.5, Claude 3.7, and Claude 4. Users are encouraged to migrate to Claude 4.5 and 4.6 to ensure continued support and optimal performance.</p>
<h2>Build better with Heroku AI</h2>
<p>The shift to a standard plan and the addition of new frontier models like Claude Opus 4.6 represent Heroku’s commitment to providing access to a wide model catalogue. By improving developer experience and expanding model choice, we are making it easier than ever to build, scale, and optimize AI-powered applications.</p>
<p>To get started, visit the <a href="https://devcenter.heroku.com">Heroku Dev Center</a> or provision the new <a href="https://elements.heroku.com/addons/heroku-inference#tab-standard">standard plan</a> for <a href="https://elements.heroku.com/addons/heroku-inference">Heroku Managed Inference and Agents</a> today.</p>
<p>The post <a href="https://www.heroku.com/blog/new-models-and-flexible-standard-plan/">Whats New in Heroku AI: New Models and a Flexible Standard Plan</a> appeared first on <a href="https://www.heroku.com">Heroku</a>.</p>
