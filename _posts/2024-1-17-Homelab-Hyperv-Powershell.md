---
layout: post
title: "Streamlining Hyper-V Lab Creation with PowerShell"
date: 2024-1-17 1:00:00 -0000
categories:
tags: [self-study, homelab, powershell]
---

Github Project: [Powershell-Lab-Hyperv](https://github.com/jacobbweber/self-study/tree/main/Powershell-Lab-Hyperv)

On a relaxed weekend, while playing around with PowerShell and sipping beers, the concept of automating a Windows domain lab setup using PowerShell sparked my interest. It became an impromptu quest to explore its possibilities. Several options like PowerShell DSC, Ansible, Terraform, and Packer crossed my mind. However, I considered the scenario where someone's requirements are straightforward and don't necessitate all that additional tooling.

As IT professionals and enthusiasts, we often find ourselves needing to set up and tear down virtual lab environments. The process can be time-consuming, especially when working with Windows domain-based labs in Hyper-V. That's where the "Powershell-Lab-Hyperv" project comes in—a PowerShell module designed to automate and simplify this process.

## Core Functions

The module offers a range of PowerShell scripts, each serving a specific purpose in the lab setup process:

For setting up and tearing down the lab environment.
- Start-LabCreation
- Start-LabDestruction

## How It Works

The module reads from .json "build" files that define the specifics of the environment you wish to create. These files include details such as the number of servers, their roles (e.g., domain controller, app server), IP configurations, and memory allocations. For example, a typical server configuration might look like this:

```json
{
    "VM": "labdc1",
    "IP": "192.168.86.50",
    "MemoryStartUpBytes": "2GB",
    "MemoryMinimumBytes": "2GB",
    "MemoryMaximumBytes": "4GB",
    "NewVHDSizeBytes": "60",
    "ProcessorCount": "1",
    "Role": "Domain Controller"
}
```

## Requirements

To use this PowerShell module, you'll need:

Hyper-V enabled on your machine.
PowerShell 7, due to dependencies in some scripts.
Terminal access with elevated privileges.

## Use Cases and Benefits

Whether you're setting up a lab for testing, development, or training, "Powershell-Lab-Hyperv" makes it easy. With just a few commands, you can have a fully functioning Windows domain-based environment, complete with multiple servers and roles.

## Future and Conclusion

While this project was initially created as a personal experiment in PowerShell and lab automation, it's worth noting that its development might not continue, with a shift towards Terraform/Ansible. Nonetheless, the "Powershell-Lab-Hyperv" module stands as a robust tool for anyone looking to quickly spin up Hyper-V labs without the manual overhead.

Enjoy a more streamlined approach to lab management with "Powershell-Lab-Hyperv"!