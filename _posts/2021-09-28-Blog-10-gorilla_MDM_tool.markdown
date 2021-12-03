---
layout: post
title:  "Blog-10-Gorilla"
date:   2021-12-03 11:58:57 -0700
categories: Gorilla MDM Tool
---




<h1>Manifest</h1>
A Manifest is how you want the applications to be installed on the the device.

The manifest include managed_installs, managed_uninstalls, managed_updates, included_manifests, or catalogs.

An example is of an manifest:

<h3>Manifest</h3>
    name: test1
    managed installs:
    - Firefox
    - Chrome
    - Slack
    managed uninstalls:
    - adobe photoshop
    - adobe reader
    managed_updates:
    - Opera
    - Edge
    - Discord
    included_manifest:
    - internal
    - servers
    - printers
    catalogs:
    - production
    - dev

    Managed_installs: is a list of items that should be installed or updated if they are not already installed.
    Managed_uninstalls: is a list of items that should be removed.
    Managed_updates: is a list of items that should only be installed if they are previously installed but are out of date.
    Included_manifests: is a list of subsequent manifests that should be examined after this one (in sequence).
        this section should not have a catalog in them.
        Reccommend for all sections to have the by them selfs because if you have an unistall and manged installed or the others it will cause loop on the clients devices. The programs will install then unistall and cause more problems

    Catalogs: is a collection of catalogs that will be designed to decide how to install software (in order).

When you create a manifest you might want to name the serial naumber of you r computer and add the name to user. Each manifest will have there own profile, so when you apply them to a manged install or etc it will be much simplier.

This is a powersful section for the client simply because the server can  control the install of the program, when there is threat or bug you can manged unistall the program, if thers serciruty tool needed you can install it with the user interaction and when there is a group of devices where they need certian program you can use included manifest where you add the devices and will add the apps to the selected devices.
  