# blog.insightstream

[![Netlify Status](https://api.netlify.com/api/v1/badges/4a3d386c-0a5e-45f7-8e27-811dad4110d2/deploy-status)](https://app.netlify.com/sites/insightstreamdev/deploys)

## installation

```bash

hugo new site blog.insightstream;
cd blog.insightstream;
git init -b main;
git remote add origin https://github.com/nareshganesan/blog.insightstream.git
git remote -v
git submodule add https://github.com/nareshganesan/uBlogger.git themes/uBlogger
```

## local development
> dependencies: hugo 

```bash
hugo server --bind 0.0.0.0 --port 1313
```