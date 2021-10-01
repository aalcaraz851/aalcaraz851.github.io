---
layout: post
title:  "Blog-2-Munki-Client-Configuration"
date:   2021-09-28 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="https://www.alansiu.net/munkiguide/wp-content/uploads/2019/01/iteminmanifest01.png" alt="MSC" width="460" height="345">



<h1>Setting up your client device</h1>
Once your sever is set upu we can now set up the client so it can receive
data from the server. T

We’re done (for now) with the server. Next, we need to configure the Munki client so it knows about our server. The Munki client stores its configuration in /Library/Preferences/ManagedInstalls.plist. Unless you’ve run the Munki client before, this file won’t yet exist. We’ll use the defaults command to create it with the data we need.

sudo defaults write /Library/Preferences/ManagedInstalls SoftwareRepoURL "http://localhost/munki_repo"

We’ve told the client tools the top-level URL for the munki repo -- http://localhost/munki_repo. That’s it for the client configuration. If you'd like, check your work with

defaults read /Library/Preferences/ManagedInstalls
which will should show the setting you just made, or

sudo /usr/local/munki/managedsoftwareupdate --show-config
which would show if a .mobileconfig profile were overriding your earlier defaults write command.

The munki client is now working !

Now that both are set client and server is set up we can test the Client Software.

The commands you run in the client are :
sudo /usr/local/munki/managedsoftwareupdate 

if you need to remove the app the command is:
sudo rm –r /Applications/Firefox.app

for final step is to test if managed Software Center.app works. This App will be shown to the client will therotially have applications managed by the server.

To locate the app we can hit the command and search bar and type "Mabage software center". This will App will have any apps loaded by the server, at the moment we dont have any but in my next blog there will be more information how do import.
https://github.com/munki/munki/wiki/Demonstration-Setup