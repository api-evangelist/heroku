---
title: "Modernizing the Command Line: Heroku CLI v11"
url: "https://www.heroku.com/blog/modernizing-the-command-line-heroku-cli-v11/"
date: "Thu, 19 Mar 2026 22:29:49 +0000"
author: "Eric Black"
feed_url: "https://www.heroku.com/feed/"
---
<p>Heroku CLI v11 is now available. This release represents the most significant architectural overhaul in years, completing our migration to ECMAScript Modules (ESM) and oclif v4. This modernization brings faster performance, a new semantic color system, and aligns the CLI with modern JavaScript standards.</p>
<p>While v11 introduces breaking changes to legacy namespaces, the benefits are substantial: better performance, improved maintainability, and enhanced usability that simplifies how you manage Heroku resources from the command line.<br />
<span id="more-18817"></span></p>
<h2>Modern architecture built for performance and usability</h2>
<h3>Faster execution via ECMAScript Modules (ESM)</h3>
<p>The transition to a full ESM-first architecture is the core of v11. By converting every command, library, and test from CommonJS to ESM, we’ve unlocked significant performance gains:</p>
<ul>
<li><strong>Superior tree-shaking</strong>: Reduced bundle sizes lead to a leaner installation and faster updates.</li>
<li><strong>Faster command execution</strong>: Optimized module loading streamlines the internal execution path.</li>
<li><strong>Modern ecosystem alignment</strong>: The CLI now mirrors the standards of modern JavaScript, simplifying long-term maintenance.</li>
</ul>
<h3>Streamlined performance with Open CLI Framework (oclif) v4</h3>
<p>We&#8217;ve jumped two major versions to oclif v4, bringing the CLI in line with the latest standards of the <a href="https://oclif.io/">Open CLI Framework</a>. This transition delivers:</p>
<ul>
<li><strong>Faster command loading</strong>: Improved manifest caching ensures the CLI doesn&#8217;t have to parse every command for every interaction, making the experience significantly faster.</li>
<li><strong>Seamless interoperability</strong>: Version 11 ensures smooth compatibility between CommonJS and ESM plugins, allowing for a more flexible developer experience.</li>
<li><strong>Modular code organization</strong>: The upgrade to oclif v4 enables granular imports, leading to a leaner and more maintainable codebase.</li>
</ul>
<p>To support these changes, we&#8217;ve also simplified our build system—migrating from Yarn to npm and removing the monorepo structure in favor of a single, more maintainable package.</p>
<h3>Enhanced visual experience</h3>
<p>Usability in v11 extends to how you interact with and interpret terminal data. The CLI’s visual output is now more intuitive, customizable, and accessible:</p>
<ul>
<li><strong>Consistent semantic colors</strong>: Common Heroku resources, success, warning, and error messages now follow a unified color palette, making it easier to identify critical information at a glance.</li>
<li><strong>Modern theme support</strong>: With Version 11, the Heroku CLI is now themeable, allowing for a more modern and readable visual experience. You can also manually opt for a basic ANSI color scheme by setting the <code>HEROKU_THEME=simple</code> env var.</li>
<li><strong>Global accessibility</strong>: Version 11 supports disabling colors entirely by setting the <code>NO_COLOR=true</code> env var for users with visual impairments or those who prefer plain-text logging.</li>
</ul>
<h3>Node.js 22 support</h3>
<p>The Heroku CLI v11 ships with Node.js 22 while maintaining Node.js 20 compatibility, providing several key benefits:</p>
<ul>
<li><strong>Modern runtime access</strong>: Users can now leverage the latest JavaScript features and performance improvements provided by the Node.js 22 runtime.</li>
<li><strong>Latest standard alignment</strong>: The update ensures the CLI remains current with the evolving JavaScript ecosystem.</li>
<li><strong>Performance-first foundation</strong>: Supporting the latest LTS version of Node.js is essential for delivering the performance gains of our new ESM-first architecture.</li>
</ul>
<h2>New commands for modern Heroku workflows</h2>
<p>We have also focused on the day-to-day developer experience. These updates refine how you interact with your Heroku resources and make it easier to discover the tools you need:</p>
<ul>
<li><strong>Unified data maintenance</strong>: The <code>heroku data:maintenance:*</code> commands are now built into the core CLI. Note that legacy <code>heroku pg:maintenance</code> and <code>heroku redis:maintenance</code> commands have been deprecated.</li>
<li><strong>Fast command discovery</strong>: Can&#8217;t remember a command name? <code>heroku search</code> helps you find it fast.</li>
<li><strong>Global prompt support</strong>: The <code>--prompt</code> flag is now available globally and appears in help text for all commands that support it.</li>
<li><strong>Streamlined REPL invocation</strong>: Access to REPL is now accessible via <code>heroku repl</code> and included in our CLI documentation and help text. Try it out!</li>
</ul>
<h2>Transitioning to Heroku CLI v11</h2>
<p>To support this new architecture, v11 includes a few updates to how certain commands and outputs behave. While these represent a shift from legacy versions, they are designed to make your workflow cleaner and more consistent:</p>
<ul>
<li><strong>Output formatting</strong>: CLI output format has changed in v11, with the most visible changes in table formatting.</li>
<li><strong>AI plugin</strong>: To keep the core installation lean and fast, the <code>heroku-cli-plugin-ai</code> is now an optional installation rather than being bundled by default.</li>
<li><strong>Unified maintenance commands</strong>: We’ve simplified data management by moving maintenance tasks into the core <code>data:maintenance:*</code> namespace. This replaces the legacy <code>pg:maintenance</code> and <code>redis:maintenance</code> commands with a single, intuitive workflow.</li>
</ul>
<h2>A modernized CLI for a modern ecosystem</h2>
<p>Heroku CLI v11 is a complete technical modernization designed to grow with the JavaScript ecosystem, and represents a major investment in the CLI&#8217;s future. By modernizing our architecture with ESM and oclif v4, we&#8217;ve built a faster, more maintainable foundation that will enable us to ship features more quickly while improving the developer experience.<br />
<a href="https://devcenter.heroku.com/articles/heroku-cli-commands#heroku-update-channel">Upgrade</a> today or visit the <a href="https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli">installation guide</a>. For a full list of updates, check out the <a href="https://github.com/heroku/cli/blob/main/CHANGELOG.md">CLI changelog</a>. As always, we welcome your feedback as we continue to improve the developer experience.</p>
<p>The post <a href="https://www.heroku.com/blog/modernizing-the-command-line-heroku-cli-v11/">Modernizing the Command Line: Heroku CLI v11</a> appeared first on <a href="https://www.heroku.com">Heroku</a>.</p>
