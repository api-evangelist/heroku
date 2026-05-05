---
title: "Behind the Scenes: How Maintaining Cloud Native Buildpacks Powers Platforms Like Heroku"
url: "https://www.heroku.com/blog/how-maintaining-cloud-native-buildpacks-powers-platforms-like-heroku/"
date: "Tue, 17 Mar 2026 15:00:03 +0000"
author: "Juan Bustamante"
feed_url: "https://www.heroku.com/feed/"
---
<p>Most developers never see the 11 pack releases we shipped in the last 14 months as <a href="https://github.com/buildpacks/pack">pack CLI</a> maintainers. That&#8217;s actually a good sign—it means the infrastructure just works. When a critical vulnerability emerges requiring an immediate upgrade, the fix is shipped within days.</p>
<p>Here&#8217;s what most developers don&#8217;t see: that same security patch now protects every buildpack user across Heroku, Google Cloud, Openshift, VMware Tanzu, and thousands of internal platforms.</p>
<p><span id="more-18767"></span></p>
<h2>The daily work of platform maintenance</h2>
<p>As maintainers of pack CLI, the entry point to Cloud Native Buildpacks (CNBs), our work lives in that invisible layer between developers and infrastructure. The routine looks like this: daily Slack monitoring, triaging GitHub issues, reviewing community pull requests, and participating in weekly Cloud Native Community Foundation (CNCF) working group meetings.</p>
<p>In the last 14 months, we&#8217;ve shipped 27 releases across CNB projects (11 for pack, 16 for buildpacks/github-actions), reviewed 65+ community PRs, and implemented two major features: Execution Environments and System Buildpacks. That&#8217;s roughly one release every 5-6 weeks, each bringing bug fixes, security patches, or new capabilities.</p>
<p>The work includes unglamorous but critical tasks: migrating Windows CI from Equinix LCOW to GitHub-hosted runners, upgrading from docker/docker to moby/moby client, and shipping FreeBSD binaries for broader platform support. When multi-arch builds needed the <code>--append-image-name-suffix</code> flag or when the Platform API 0.14 lifecycle restorer had issues, those fixes went out to everyone.</p>
<p>There are no flashy demos; instead this is invisible infrastructure work that proves its worth when an emergency security patch ships or a build completes in 30 seconds instead of failing after 5 minutes.</p>
<h2>How upstream open source creates downstream value</h2>
<p>Here&#8217;s where it gets interesting: Heroku has funded our maintainer work, but the benefits ripple across the entire cloud-native ecosystem. This bidirectional value is what makes open source infrastructure so powerful.</p>
<p>Take <a href="https://github.com/buildpacks/pack/pull/2349">System Buildpacks</a>, a feature we recently implemented:</p>
<ul>
<li>For <strong>Heroku</strong>, it means they can curate platform defaults while giving users flexibility with third-party buildpacks.</li>
<li>For <strong>Google Cloud Run</strong>, it solves its buildpack composition problem.</li>
<li>For <strong>internal platform teams</strong>, it eliminates the manual Procfile buildpack overhead that&#8217;s been a pain point for years.</li>
</ul>
<p>That one newly implemented feature created universal benefit.</p>
<p>Or consider <a href="https://github.com/buildpacks/pack/pull/2324">Execution Environments</a>, another major feature we shipped this year. This enables Heroku to support test environments for CI products while also helping any platform operator who needs consistent build configurations across development, CI, and production. The code lives upstream in the CNCF project, battle-tested by multiple companies, and maintained collaboratively.</p>
<p>The CNCF governance model ensures no single company can control the direction. Companies like Heroku, Google, and VMware collaborate on infrastructure so they can compete on developer experience. When we fix a multi-arch publishing bug or add FreeBSD support, everyone benefits immediately.</p>
<h2>Real innovation happens in production</h2>
<p>The features we&#8217;re shipping aren&#8217;t theoretical, they solve real problems in production:</p>
<ul>
<li><a href="https://github.com/buildpacks/rfcs/blob/main/text/0131-build-observability.md"><strong>Build Observability (RFC 0131)</strong></a>: Platform operators need metrics and tracing to optimize costs and troubleshoot failures. Coming in Q3 2026, this will provide comprehensive visibility into build performance across the ecosystem.</li>
<li><a href="https://github.com/buildpacks/rfcs/blob/main/text/0130-oci-image-annotations.md"><strong>OCI Image Annotations (RFC 0130)</strong></a>: Enterprise compliance requires metadata tracking. We&#8217;re making it zero-config so platforms can meet SOC2, FedRAMP, and other regulatory requirements without manual overhead.</li>
<li><a href="https://github.com/buildpacks/rfcs/blob/extract-extender/text/0000-extract-extender.md"><strong>Removing Kaniko dependency</strong></a>: Supply chain security isn&#8217;t just buzzwords, it&#8217;s actively removing unmaintained dependencies from critical infrastructure to reduce risk.</li>
</ul>
<p>Each feature starts with a production requirement, gets refined through community discussion, and ships as a standard that everyone can rely on.</p>
<h2>Why this model works</h2>
<p>At KubeCon EU 2025, the biggest question during our presentation &#8220;<a href="https://www.youtube.com/watch?v=Eb9AweCazi8">Buildpacks: Pragmatic Solutions to Quick and Secure Image Builds</a>&#8221; wasn&#8217;t about technical implementation—it was about sustainability. How do we keep critical open source infrastructure maintained?</p>
<p>Companies like Heroku invest in dedicated maintainer teams, and get battle-tested technology that serves their needs while contributing to the commons. The ecosystem gets features driven by real production requirements, not academic speculation, and developers get reliable infrastructure that just works.</p>
<p>That&#8217;s the true impact of open source maintainership: 65+ PRs reviewed, 27 releases shipped, 2 major features delivered, and the countless invisible fixes that keep platforms running smoothly.</p>
<h2>Join the conversation at KubeCon EU 2026</h2>
<p>The evolution of Cloud Native Buildpacks continues, and there is no better place to see where we’re headed next than at KubeCon EU 2026.</p>
<p>If you want to dive deeper into the future of the project, don’t miss the upcoming session:</p>
<p><a href="https://kccnceu2026.sched.com/event/2EF5w?iframe=no"><strong>Buildpacks: Towards 1.0, AI, and Other Things</strong></a><br />
Thursday March 26, 2026 14:30 &#8211; 15:00 CET<br />
Aidan Delaney, Bloomberg</p>
<p>This talk covers the road to 1.0, focusing on the stability and technical components (Lifecycle, Platform, and Builder) necessary for a production-ready foundation. Aidan will also showcase how the ecosystem is integrating AI and Machine Learning to simplify the deployment of AI-driven applications.</p>
<h2>Visit the Buildpacks Project booth</h2>
<p>The community will be out in full force! Stop by the CNB booth, P-3B in the Project Pavilion (<a href="https://events.linuxfoundation.org/kubecon-cloudnativecon-europe/features-add-ons/project-engagement/#project-pavilion-map">map</a>), to meet the maintainers, ask questions, and learn more about the &#8220;invisible&#8221; infrastructure powering your code. We’d love to see you there!</p>
<p>The post <a href="https://www.heroku.com/blog/how-maintaining-cloud-native-buildpacks-powers-platforms-like-heroku/">Behind the Scenes: How Maintaining Cloud Native Buildpacks Powers Platforms Like Heroku</a> appeared first on <a href="https://www.heroku.com">Heroku</a>.</p>
