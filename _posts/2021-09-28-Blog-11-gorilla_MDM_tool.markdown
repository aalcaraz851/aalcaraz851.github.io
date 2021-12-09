---
layout: post
title:  "Blog-11-Gorilla"
date:   2021-12-10 11:58:57 -0700
categories: Munki MDM Tool
---

<h1>How to Install Chocolatey</h1>
Step1.

      Before installing this application you have to chekc if you have the right Requirement:
       Windows 7+ / Windows Server 2003+
      PowerShell v2+ (minimum is v3 for install from this website due to TLS 1.2 requirement)
      .NET Framework 4+ (the installation will attempt to install .NET 4.0 if you do not have it installed)(minimum is 4.5 for install from this website due to TLS 1.2 requirement)

Step2:
YOu can download this using Ansible, Chef, PS DSC and Puppet.
we will be donwloading this for individual use.

      a) we will use powershell and run as administrtor
      b)install using powershell
        - If you're using PowerShell, make sure Get-ExecutionPolicy isn't Restricted. We recommend utilizing Bypass to get items installed without having to deal with the policy, or AllSigned for a lot more security.

        - Run Get-ExecutionPolicy. If it returns Restricted, then run Set-ExecutionPolicy AllSigned or Set-ExecutionPolicy Bypass -Scope Process.
      c) Run the command:
        - Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

        - Press Enter after pasting the pasted content into your shell.
        - Wait a 5 mins for the command to install.
        - If you're not seeing any issues, Chocolatey is good to just use! Now type choco or choco -? to get started, or go to Getting Started for more information.    
    
Your now ready to use chocolatey!

You can also install using Gorilla

<h1>Install Chocolatey With Gorilla</h1>
      1. https://chocolatey.org/install.ps1 is the link to the powershell script.
      2. Obtain the file's SHA256 hash.
      3.Make an entry in your catalogue that looks like this:



Chocolatey:
   display_name: Chocolatey
   check:
    file:
      - path: C:\ProgramData\chocolatey\choco.exe
   installer:
    hash: 1cf9d9364b2bd8748dc3038db7053e72e31382b5bac0c91afa43e86e72d9d620
    location: packages/chocolatey/chocolatey_installer-1.0.ps1
    type: ps1
   version: 1.0

Additionally, you can specify the choco binary's edition. If a newer version of the software has been downloaded, Gorilla would not restore it.

   check:
     file:
       - path: C:\ProgramData\chocolatey\choco.exe
         version: 0.10.11.0



<h1>Chocolatey Extensions</h1>
Certain applications may also necessitate the use of chocolatey extension such as Google Chrome and firefox. You might wish to give Gorilla permission to install it as well.

   ChocolateyCoreExtension:
     dependencies:
      - Chocolatey
    display_name: Chocolatey Core Extension
      check:
      file:
      - path: C:\ProgramData\chocolatey\extensions\chocolatey-core\chocolatey-core.psm1
        hash: 376E6EDA567DDDD6AA70CFC9EC5380CE0EB1383BE83C2FBDC87F6FC79252E4E8
    installer:
        hash: ed7a281f45a61150df0e1414651bca8501004c56deb43439c075f1ba58aff70a
        location: packages/chocolatey/extensions/core/chocolatey-core.extension.1.3.3.nupkg
        type: nupkg
        version: 1.3.3
When it comes to extensions, the SHA256 hash of the.psm1 file will almost certainly be your arbiter of facts.
