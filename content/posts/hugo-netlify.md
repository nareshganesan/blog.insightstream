---
title: "Hugo + Netlify = awesome!"
date: 2021-02-26T00:54:35+05:30
lastmod: ""
draft: false
categories: ["hugo", "ci/cd", "jamstack"]
tags: ["hugo", "netlify", "ci/cd", "jamstack"]
---

Hugo and Netlify have really simplified the job for creating a website (static) quickly.

## Hugo

Some of my favorite features which make hugo really standout are below

- Simple markdown based rendering
- REST api support (makes serving dynamic data)
- Javascript theme support
- Ease of Deployment (mainly github and netlify)
- Live reload

We can simply focus on the content and not worry about web layout or design as there are plenty of preconfigured themes to choose. It is also relevantly easy to customise an existing theme or build one from scratch. I prefer to use a theme out of the box to save time.

## Netlify

Netlify has made deployment super simple. For starters it supports github/gitlab/bitbucket for scm, by default netlify deploys to its subdomain and they also support custom domain.

- Free hosting
- Built-in CI/CD
- Domains & DNS management
- Auto TLS certificate management using Let's encrypt

My current domain provider is google but I have transferred the DNS settings to Netlify so I can use their auto deployment and tls management. There is only one downside to this setup, since I had to manage Google Workspace MX records in netlify's DNS settings.
