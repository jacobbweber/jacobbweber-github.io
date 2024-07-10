---
layout: post
title: "Homelab on Hyper-V"
date: 2024-4-17 1:00:00 -0000
categories:
tags: [Homelab]
---

Github Project: [Homelab](https://github.com/jacobbweber/homelab)

## Overview

I'm ready to kick off my homelab project after months of contemplation and research. My objective is to adopt modern methodologies like [Infrastrucutre-as-code](https://en.wikipedia.org/wiki/Infrastructure_as_code) and [GitOps](https://codefresh.io/learn/gitops/#:~:text=GitOps%20is%20an%20operational%20framework,infrastructure%20and%20manages%20software%20deployment.) to streamline the setup, management, and updating of self-hosted services in my homelab.

Ultimately, this project will establish a robust infrastructure foundation that facilitates the exploration of new technologies and concepts, mirroring common setups found in professional environments.

I plan to document this journey in a series of blog posts that will delve into the specifics of the project. These posts will explore my thought processes and the rationale behind various decisions throughout the project. I hope this will help others who struggle with just getting started or inspire ideas for their own projects. I also welcome feedback and collaboration! 

### Getting Started

There were some easy assumptions to be made on where to start. I knew I would need hardware, a hypervisor, and version control. The first two are easy since I plan to use (for now) my Gaming PC and Hyper-V. As for version control I already have some projects in GitHub so decided to go that route, although Gitlab was another consideration.

Before I jump into playing with Hyper-V and VMs. I wanted to come up with some version control strategies and a branching model to break down the work into smaller pieces. I want to land somewhere between not boiling the ocean and not just commiting to main with commit messages like "Big Time Changes".

After doing some research and of course boiling the ocean :) I decided to just adopt [Semantic Versioning](https://semver.org/), [Conentional Commits](https://www.conventionalcommits.org/en/v1.0.0/), and [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow).

### Setting up the GitHub project

Create the project

- Created Project: Github Project: [Homelab](https://github.com/jacobbweber/homelab)
- Created develop branch
- Setup self-hosted runner

Implement automatic versioning, using semantic-release

- Pull project
- Create github action:
```shell
mkdir .github/workflows/
touch semantic-release.yml # refer to project to see file contents
```
- Install node.js on machine where github runner is running.
- Initialize new Node.js project, and install plugins

```shell
npm init -y # will generate package.json with default values.
npm install semantic-release --save-dev # install
npm install @semantic-release/commit-analyzer --save-dev #install plugins
npm install @semantic-release/release-notes-generator --save-dev #install plugins
npm install @semantic-release/git --save-dev #install plugins
npm install @semantic-release/github --save-dev #install plugins
npm install @semantic-release/changelog --save-dev #install plugins
```
- Configure package.json
- Create and configure release.config.js.
> The release.config.js file is optional, if you want more customized configuration, like emojis in your release notes based on commit message.
{: .prompt-info }
- Add and push changes

>Below are some short hand notes to a few common git commands ill use frequently.
{: .prompt-info }
```shell
git clone 'projecturl'
git add *
git add .gitignore
git add .github/*
git commit -am 'Initial Commit'

git fetch --all # Make sure your local repo is up to date with all remote branches
git checkout develop # Switch to develop branch
git branch --set-upstream-to=origin/develop develop # Track the remote branch and set it as upstream
git pull # pull latest changes

#To merge hotfix or changes or releases to main back into develop, shouldnt happen often in my workflow for this project
git checkout main
git pull origin main
git checkout develop
git pull origin develop
git merge main
git commit
```

### Starter Setup

- Hardware: [My PC](https://jacobbweber.com/my-office/#setup)
- Hypervisor: Hyper-V
- Version Control: Github [Homelab](https://github.com/jacobbweber/homelab)

### Tech Stack

- Metal
    - Hyper-V
- Platform
    - HashiCorp Packer
    - HashiCorp Terraform
    - Ansible
    - Chocolatey
    - Microsoft Core INF, like: Active Directory, DNS, DHCP
    - k3 Kubernetes
- System
    - Grafana
    - Prometheus
    - Password managers.
- App

## Metal Setup

- In my first iteration of this Homelab, I plan to just use my main PC for hardware, and run hyper-v. Since this requires running some powershell as administrator and the script is relatively small, I am just going to run it manually (breaking my gitops methodology) at this phase. In the future when i have some dedicated hardware, I plan to use gitops like tooling to provision the bare metal setup.

- Created an Issue, assigned it to myself, added some details and a label
- Created a feature branch off of this issue, using source as develop (trying to not commit directly to main to develop good habbits and honor the semantic versioning plan)
- Once branch was created, I ran:

```shell
git fetch origin
git checkout 1-create-a-hyper-v-setup-script
```