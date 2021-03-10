---
title: "Hugo + Netlify = awesome!"
date: 2021-02-26T00:54:35+05:30
lastmod: ""
draft: false
categories: ["hugo", "ci/cd", "jamstack"]
tags: ["hugo", "netlify", "ci/cd", "jamstack"]
---

Hugo and Netlify have really simplified the job for creating a website (static) quickly. Hugo makes content creation as simple as editing markdown files. Web hosting, deployment and TLS management are taken care by Netlify. By making content creation pipeline simple, flexibility to choose from plethora of themes and ease of deployment makes the combo really useful. There are other competitors like Next.js, Gatsby, jekyll, Nuxt etc. Some scenarios where Hugo and Netlify can really make a difference are listed below.

{{< admonition type=note >}}

- personal blog
- designer portfolio
- blog for business
- documentation site for tools
- Wiki docs

{{< /admonition >}}

## Hugo and Netlify setup

Let's try to understand what makes this combination really useful. Hugo is static site generator primarily based on Markdown for creating content. The Site can be customised using predefined themes from community or creating one from scratch. Once the hugo site is ready, deployment is as easy as commiting files to github. This is where Netlify comes into play. Lets review the steps to get started with the combination

{{< admonition type=tip >}}

- Install golang
- Install hugo and theme
- Create content using markdown files
- Create a netlify account
- Create a github repo
- Commit and deploy website to netlify subdomain (domain can also be done by configuring DNS with netlify)

{{< /admonition >}}

The following installation steps are verified against Ubuntu 18.04

### 1. Install Golang

```shell
# download golang binary
wget https://dl.google.com/go/go1.13.linux-amd64.tar.gz
# extract
sudo tar -C /usr/local -xzf go1.13.linux-amd64.tar.gz
# add to system path
export PATH=$PATH:/usr/local/go/bin
source ~/.bashrc
# verify installation
go version
```

### 2. Install Hugo and theme

```shell
# setup a src repo for golang / hugo
mkdir $HOME/src
cd $HOME/src
# clone hugo source repo
git clone https://github.com/gohugoio/hugo.git
cd hugo
# install hugo
# remove --tags extended (if you do not want to have scss/css)
go install --tags extended
# verify installation
hugo version
# create a static website
hugo new site static-website-name

# install hugo themes
cd static-website-name
git init
# add hugo theme as a submodule of the current project repo
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
# add theme name to config.yaml
echo theme = "ananke" >> config.toml
```

### 3. Create static content

```shell
cd static-website-name;
# to create a new post
hugo new posts/my-first-post.md
# to start hugo server
hugo server -D
```

More information about hugo is [here](https://gohugo.io/getting-started/quick-start/)

### 4. Create Netlify account

Netlify supports github/gitlab/bitbucket for account creation. After creating the account, it asks for connecting to github to read repository information, we have to login to our github account and approve netlify app with those permissions. Once done, then netlify can direclty connect to our github account and access any repository for website deployment in one of their subdomain. More information about Netlify can be found [here](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/)

### 5. Create github repo

```shell
cd static-website-name;
# add the remote repository from github
git remote add origin <remote repository URL>
# add all the changes
git add .
# commit the changes
git commit -m 'initial commit'
# push to remote repo
git push origin master

```

### 6. Deploy to Netlify

Deployment to netlify is as simple as authenticating netlify with github and selecting the github repo to build and deploy. Once the repo is selected, netlify automatically deploys the hugo application to one of hugo's subdomain (automatically created). It also manages TLS for the subdomain so we dont have to worry about security. More articles about Netlify and hugo can be found [here](https://www.netlify.com/tags/hugo/)

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
- CDN

My current domain provider is google but I have transferred the DNS settings to Netlify so I can use their auto deployment and tls management. There is only one downside to this setup, since I had to manage Google Workspace MX records in netlify's DNS settings.
