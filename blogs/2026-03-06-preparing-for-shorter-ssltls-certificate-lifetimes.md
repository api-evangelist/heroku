---
title: "Preparing for Shorter SSL/TLS Certificate Lifetimes"
url: "https://www.heroku.com/blog/preparing-for-shorter-ssl-tls-certificate-lifetimes/"
date: "Fri, 06 Mar 2026 16:50:10 +0000"
author: "Emily Huang"
feed_url: "https://www.heroku.com/feed/"
---
<p>The web browser and certificate authority industry is shortening the maximum allowed lifetime of TLS certificates. These changes will improve security on the Web, but you may have to change certificate maintenance practices for apps you run on Heroku.</p>
<p>The good news is that if you’re using <a href="https://devcenter.heroku.com/articles/automated-certificate-management">Heroku Automated Certificate Management</a>, no changes are required: Heroku already refreshes and updates certificates on your apps according to the new policies.</p>
<p>If you maintain and upload certificates for your Heroku applications yourself, here is what the changes will mean for you.</p>
<h2>Industry shift towards shorter certificate lifetimes</h2>
<p>The CA/Browser Forum <a href="https://cabforum.org/working-groups/server/baseline-requirements/documents/CA-Browser-Forum-TLS-BR-2.2.2.pdf">is phasing in shorter maximum lifetimes for all publicly trusted SSL/TLS certificates</a>. While the final goal is a 47-day limit by 2029, the first major milestone is approaching quickly.</p>
<p>Starting <strong>March 15, 2026</strong>, the maximum validity period for publicly trusted SSL/TLS certificates will be reduced to <strong>200 days</strong>.</p>
<table>
<thead>
<tr>
<th>Effective Date</th>
<th>Maximum Certificate Lifespan</th>
</tr>
</thead>
<tbody>
<tr>
<td>Current</td>
<td>398 days</td>
</tr>
<tr style="font-style: italic;">
<td><strong>March 15, 2026</strong></td>
<td><strong>200 days</strong></td>
</tr>
<tr>
<td>March 15, 2027</td>
<td>100 days</td>
</tr>
<tr>
<td>March 15, 2029</td>
<td>47 days</td>
</tr>
</tbody>
</table>
<h2>Why this is happening</h2>
<p>Shorter certificate lifespans improve security by:</p>
<ul>
<li><strong>Reduced exposure</strong>: Shrinks the window of exposure if a private key is compromised</li>
<li><strong>Modern standards</strong>: Ensures certificates rotate frequently to adopt the latest cryptographic standards</li>
<li><strong>Automation</strong>: Encourages a shift toward automated certificate management</li>
</ul>
<h2>Recommended actions for manual certificate users</h2>
<p>If you use <a href="https://devcenter.heroku.com/articles/ssl#manually-upload-certificates">custom SSL certificates</a> on Heroku (certificates you obtain and upload yourself), you will need to:</p>
<ul>
<li><strong>Plan for more frequent renewals</strong>: After March 15, 2026, you&#8217;ll need to renew certificates at least every 200 days (approximately every 6.5 months) rather than annually.</li>
<li><strong>Update your renewal processes</strong>: Ensure your team or certificate management tools can handle the increased renewal frequency.</li>
<li><strong>Check your current certificates</strong>: Review the expiration dates of your existing certificates.<em style="display: block;">Note: Certificates issued before March 15, 2026 with longer validity periods will remain valid until they expire, but renewals after that date must comply with the new 200-day maximum.</em></li>
</ul>
<h2>Automating certificate renewals with Heroku ACM</h2>
<p>Consider switching to <a href="https://devcenter.heroku.com/articles/automated-certificate-management"><strong>Heroku Automated Certificate Management (ACM)</strong></a>. ACM automatically provisions and renews certificates for your custom domains at no additional cost, eliminating the need for manual certificate management.</p>
<p>To enable ACM for your app:</p>
<pre class="language-bash"><code>heroku certs:auto:enable -a your-app-name
</code></pre>
<p>Learn more: <a href="https://devcenter.heroku.com/articles/automated-certificate-management">Heroku ACM Documentation</a></p>
<h2>Have questions about certificate management?</h2>
<p>If you have questions about these changes or need assistance with your certificate strategy, please contact Heroku Support or visit our documentation:</p>
<ul>
<li><a href="https://devcenter.heroku.com/articles/ssl">SSL Certificates on Heroku</a></li>
<li><a href="https://devcenter.heroku.com/articles/automated-certificate-management">Automated Certificate Management</a></li>
</ul>
<p>We&#8217;re committed to helping you navigate these industry changes smoothly.</p>
<p>The post <a href="https://www.heroku.com/blog/preparing-for-shorter-ssl-tls-certificate-lifetimes/">Preparing for Shorter SSL/TLS Certificate Lifetimes</a> appeared first on <a href="https://www.heroku.com">Heroku</a>.</p>
