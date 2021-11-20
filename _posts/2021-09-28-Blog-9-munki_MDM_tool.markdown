---
layout: post
title:  "Blog-9-Gorilla-Catalogs"
date:   2021-11-19 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="https://github.com/1dustindavis/gorilla/blob/main/gorilla.png" alt="MSC" width="460" height="345">



<h1>Catalogs</h1>
What are catalogs?

A catalog contains information on all of the available packages. These details instruct Gorilla on how to install or uninstall an item, as well as how to determine whether it is already installed or up to date.

Catalogs are written in yaml, and each package is represented by the package name, which is followed by a nested object containing the package details.


<h1>Supported Keys</h1>
    dependencies:

    example_dep
    display_name: Example App
    version: 1.2.3

dependencies is an optional array of package names that should be installed before this package.
display_name should be a human-readable name, but is not currently used.
version should be the version of the application, but is not currently used.

<h3>Status Checks</h3>
File Checks

check:
    file:
    - path: C:\example.exe
     hash: 
path is a path to a file that must exist for the item to be considered installed.
version is the version of the file that can be found by looking at the "Details" tab of the file's properties window.
hash is an optional sha256 of the item that is expected at install_check_path.
You can get the hash of a file with Powershell. See below for an example.

    PS C:\> Get-FileHash $pshome\powershell.exe | Format-List
    Algorithm : SHA256
    Hash      : 6A785ADC0263238DAB3EB37F4C185C8FBA7FEB5D425D034CA9864F1BE1C1B473
    Path      : C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe



<h3>Registry Checks</h3>
    check:

    registry:

    name: Example App
    version: 1.2.3

name is the DisplayName of the item, exactly as it appears in the registry under HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\.
version is the DisplayVersion of the item, exactly as it appears in the registry under HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\.

<h2>Installers</h2>
    installer:
      arguments:
     - /L=1033
     - /S
    hash: ce6c93417489d6c1f205422a4a9e8d5181d1ac24b6bcae3bd68ec225efdab12e
    location: packages/apps/example_installer.exe
    type: exe

arguments: is an optional list of arguments to pass to the installer. Currently only supported by exe installers.
hash: is a required sha256 hash of the file located at location.
location: is required and should be the path to the package, relative to the url provided in the configuration file.
type: is required type of installer located at location and can be nupkg, msi, exe, or ps1.


<h2>Uninstallers</h2>
    uninstaller:
     arguments:
     - /S
     - /noreboot
    hash: f3b4bb8bc7d47036674c1ed04713c720530f180e08da786fbcaf34c18be18dca
    location: packages/apps/example_uninstaller.exe
    type: exe

arguments: similar to installer: arguments, but used when the item is configured as a managed_uninstall.
hash: similar to installer: hash, but used when the item is configured as a managed_uninstall.
location: similar to installer: location, but used when the item is configured as a managed_uninstall.
type: similar to installer: type, but used when the item is configured as a managed_uninstall.

<h1>Example Catalog:</h1>
---
    GoogleChrome:
      display_name: Google Chrome
      check:
        registry:
          name: Google Chrome
          version: 68.0.3440.106
      installer:
        hash: ce9c44417489d6c1f205422a4b9e8d5181d1ac24b6dcae3bd68ec315efdeb18b
        location: packages/google-chrome/GoogleChrome.68.0.3440.106.nupkg
        type: nupkg
      version: 68.0.3440.106

    ColorPrinter:
      dependencies:
        - Canon-Drivers
      display_name: Color Printer
      installer:
        hash: a8b4ff8bc7d77036644c1ed04713c550550f180e08da786fbca784818b918dac
        location: packages/colorprinter.1.0.nupkg
        type: nupkg
      version: 1.0

    CanonDrivers:
      display_name: Canon Printer Drivers
      installer:
        hash: ca784818b91850f180e08da786ac1ed04713c5a8b4ff8bc7d77036644dac505aec
        location: packages/Canon-Drivers.1.0.nupkg
        type: nupkg
      version: 1.0

    Chocolatey:
      display_name: Chocolatey
      check:
        file:
          - path: C:\ProgramData\chocolatey\bin\choco.exe
            hash: bd82a10e75c5be624d916557b3d711a867d40bedd7b9e4be862eadb74f622e37
      installer:
        location: packages/chocolatey/chocolateyInstall.ps1
        hash: 38cf17a230dbe53efc49f63bbc9931296b5cea84f45ac6528ce60767fe370230
        type: ps1
      version: 1.0

    ChefClient:
      display_name: Chef Client
      check:
        script: |
          $latest = "14.3.37"
          $chefPath = "C:\opscode\chef\bin\chef-client.bat"
          If (![System.IO.File]::Exists($chefPath)) {
            exit 0
          }
          $current = C:\opscode\chef\bin\chef-client.bat --version
          $current = $current.Split(" ")[1]
          $upToDate = [System.Version]$current -ge [System.Version]$latest
          If ($upToDate) {
            exit 1
          } Else {
            exit 0
          }
      installer:
        location: packages/chef-client/chef-client-14.3.37-1-x64.msi
        hash: f5ef8c31898592824751ec2252fe317c0f667db25ac40452710c8ccf35a1b28d
        type: msi
      uninstaller:
        location: packages/chef-client/chef-client-14.3.37-1-x64.msi
        hash: f5ef8c31898592824751ec2252fe317c0f667db25ac40452710c8ccf35a1b28d
        type: msi
      version: 14.3.37

    vlc:
      display_name: VLC
      check:
        file:
          - path: C:\Program Files (x86)\VideoLAN\VLC\vlc.exe
            version: 3.0.3
      installer:
        location: packages/apps/vlc/vlc-3.0.3-win32.exe
        hash: 65bf42b15a05b13197e4dd6cdf181e39f30d47feb2cb6cc929db21cd634cd36f
        arguments: 
         - /L=1033
         - /S
        type: exe
      uninstaller:
        location: packages/apps/vlc/vlc-3.0.3-uninstall.exe
        hash: 676dcb69da99728feb8af3231e863dbb9639dc09f409749a74dd5c08dc2fb809
        arguments: 
         - /S
        type: exe
      version: 3.0.3
