---
title: "Installing a *.Msixbundle File"
date: 2020-11-24T11:14:43-05:00
comments: true
categories: 
- info
tags:
- Windows Store
- msixbundle
- workaround
- install
---

This is a pain in the ass. My user profile is prevented from accessing the "Windows Store" by my administrator, because they're dumb I guess. I dunno. It's really not a clever move if you think about it, because you're ensuring that people source their software from places other than "vetted distribution sites" such as Windows Store. But, whatever. This is the workaround. All you're required to do is open powershell and execute the command `Add-AppxPackage file.msixbundle`. That's pretty much it. You may want to do so as administrator, that way the bundle you install is available to everyone who uses the computer, but I'm sure it doesn't matter either way.
