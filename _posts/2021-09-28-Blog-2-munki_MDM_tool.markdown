---
layout: post
title:  "Blog-2-Munki-Client-Configuration"
date:   2021-09-28 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="https://www.alansiu.net/munkiguide/wp-content/uploads/2019/01/iteminmanifest01.png" alt="MSC" width="460" height="345">



<h1>Setting up your client device</h1>
Once your sever is set up we can now set up the client so it can receive
data from the server like Apps, security tools and much more. This can be a very powerful tool to use when managing over 1000 device at a time, this can update packages, programs, and download whats needed.
<h2>1.</h2>
The server is (for the time being) shut down. The Munki client must then be configured to recognize our server. /Library/Preferences/ManagedInstalls.plist is where the Munki client saves its settings. This file will not exist unless you've already executed the Munki client. To populate it with the information we require, we'll use the defaults command.

sudo defaults write /Library/Preferences/ManagedInstalls SoftwareRepoURL "http://localhost/munki_repo"
<h2>2.</h2>
We've given the client utilities the munki repo's upper URL. -- http://localhost/munki_repo. That's all there is to the client setup. If you like, you can double-check your work with:

defaults read /Library/Preferences/ManagedInstalls
which will should show the setting you just made, or

sudo /usr/local/munki/managedsoftwareupdate --show-config
which would show if a .mobileconfig profile were overriding your earlier defaults write command.

The munki client is now working !
<h2>3.</h2>
We may now test the Client Software after both the client and server have been set up.

The commands you run in the client are :
sudo /usr/local/munki/managedsoftwareupdate 

if you need to remove the app the command is:
sudo rm –r /Applications/Firefox.app
<h2>4.</h2>
The final step is to test if managed Software Center.app works. This App will be shown to the client will therotially have applications managed by the server.

<h2>5.</h2>
To locate the app we can hit the command and search bar and type "Manage software center". This will App will have any apps loaded by the server, at the moment we dont have any but in my next blog there will be more information how do import.
https://github.com/munki/munki/wiki/Demonstration-Setup