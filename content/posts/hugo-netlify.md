---
title: "Hugo + Netlify = awesome!"
date: 2021-02-26T00:54:35+05:30
lastmod: ""
draft: false
categories: ["hugo", "ci/cd", "jamstack"]
tags: ["hugo", "netlify", "ci/cd", "jamstack"]
---

Hugo and Netlify have really simplified the job for creating a website (static) quickly. Some of scenarios where Hugo and Netlify can really make a difference.

{{< admonition type=note >}}

- personal blog
- designer portfolio
- blog for business
- documentation site for tools

{{< /admonition >}}

Let's try to understand what makes this combination really useful. Hugo is static site generator primarily based on Markdown for creating content. The Site can be customised using predefined themes from community or creating one from scratch. Once the hugo site is ready, deployment is as easy as commiting files to github. This is where Netlify comes into play. Lets review the steps to get started with the combination

{{< admonition type=tip >}}

- Install golang
- Install hugo
- Create a netlify account
- Create a github repo

{{< /admonition >}}

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
