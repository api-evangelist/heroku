---
title: "Learn How to Lower Heroku Dyno Latency through Persistent Connections (Keep-alive)"
url: "https://www.heroku.com/blog/learn-how-to-lower-heroku-dyno-latency-keep-alive/"
date: "Tue, 04 Nov 2025 16:27:37 +0000"
author: "Richard Schneeman"
feed_url: "https://blog.heroku.com/feed/"
---
The Performance Penalty of Repeated Connections Before the latest improvements to the Heroku Router, every connection between the router and your application dyno risked incurring the latency penalty of a TCP slow start. To understand why this is a performance bottleneck for modern web applications, we must look at the fundamentals of the Transmission Control […] The post Learn How to Lower Heroku Dyno Latency through Persistent Connections (Keep-alive) appeared first on Heroku .
