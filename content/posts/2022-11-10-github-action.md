---
title: "Github Actions"
date: 2022-11-10T16:40:01-05:00
---

It's a little excessive for this site, but researching various automation options led me to glue a Hugo CLI install and build template provided by GitHub to a
[Neocities Github Action](https://jonathanchang.org/blog/deploying-your-static-site-to-neocities-using-github-actions/#adding-your-neocities-api-token). It took a couple of tries to get the pieces together and GitHub's Node.js 12 warning isn't the most reassuring thing, but deploy on commit works.