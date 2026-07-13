---
title: "Securing Heroku CLI Credentials with System Keychain Storage"
url: "https://www.heroku.com/blog/securing-heroku-cli-credentials-with-system-keychain-storage/"
date: "2026-07-01"
author: ""
feed_url: "https://www.heroku.com/blog/feed/"
---
Starting with version 11.8.0, the Heroku CLI will store authentication credentials in system keychains by default rather than .netrc files. This leverages OS-native secure storage while maintaining backward compatibility for existing workflows.
