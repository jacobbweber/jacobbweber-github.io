---
layout: post
title: "Creating a self-study website using Godaddy, Github Pages, and Jekyll"
date: 2023-12-25 9:49:00 -0000
categories:
tags: [self-study, homelab]
---

Github Project: [jacobbweber.github.io](https://github.com/jacobbweber/jacobbweber-github.io)

It's been years since I created a website. A decade ago I would have hosted an internal server at home, likely IIS, and made it publicly available. I wanted to find a cheaper and slightly easier solution. After some research I came across jekyll and github pages. This was perfect for my needs. I could write documentation in markdown stored in github and poof, its a website.

Below are shorthand notes and general overview on how I made my own site.

## Overview

- Optionally - Purchase a domain using [GoDaddy](https://www.godaddy.com/) Domain: jacobbweber.com
    > If you do not wish to pay, you can do this for free but your URL will be yourgithubproject.github.io. My domain was so cheap plus the benefit of free email contact@jacobbweber.com, the cool factor seemed worth it. Eventually I will look into using [Cloudflare](https://www.cloudflare.com/) as a provider instead of GoDaddy.
    {: .prompt-tip }

- Researched [Jekyll Resources](https://jekyllrb.com/)
- Github Pages [Gitjub Pages](https://pages.github.com/) also see: [Github + Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)

## Steps

- I chose the free "[Chirpy](https://chirpy.cotes.page/posts/getting-started/)" jekyll theme - review installation options and choose what works for you.
- I created a github project, my project is [jacobbweber.github.io](https://github.com/jacobbweber/jacobbweber.github.io)
- In the project's Settings
  - Go to "Pages" section
    - Change Build and Deployment source, from "Branch", to "Github Actions"
    - If you bought a custom domain, also configure the "Custom Domain" option on this same page and follow the steps it provides to verify and configure DNS for your domain.
- Update the _config.yml file to include your own details.
- Commit your changes and this should trigger the deployment. (Check your github projects deployment progress and output)
- Navigate to https://yourprojectname.github.io to see your website.
  > Go back to your pages subsection under Settings to find your URL.
  {: .prompt-tip }

## References

Template Documentation: <https://chirpy.cotes.page/>
