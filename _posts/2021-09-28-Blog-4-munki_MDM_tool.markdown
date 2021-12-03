---
layout: post
title:  "Blog-4-Munki-Admin-Configuration"
date:   2021-10-13 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="http://www.amsys.co.uk/wp-content/uploads/munki-admin-packages-java.png" alt="MSC" width="460" height="345">



<h1>UsingAdmin</h1>
So far, we've been using command-line tools to manage the Munki server, and sometimes the
command-line is the best way to go (for munkiimport, for example), but for a lot of the
changes we make, a graphical user interface (GUI) tool is best.


<h1>Installing MunkiAdmin</h1>
Grab the latest MunkiAdmin release from
https://github.com/hjuutilainen/munkiadmin/releases/latest

Once the .dmg is downloaded, double-click it, and then drag MunkiAdmin.app to your
/Applications folder

<h1>Configuring MunkiAdmin</h1>
When MunkiAdmin first opens, it will likely ask you to select a repo. Press Cmd-Shift-G and
then go to /Users/Shared/munki_repo

Most importantly, you now should go to MunkiAdmin > Preferences and then make sure you
select On Startup > Open previous repository, so MunkiAdmin won't prompt you for a new
repo every time.

Now you can use MunkiAdmin to add new catalogs, add new manifests, add items to or
remove items from various manifests.
For importing new items, you'll still want to use munkiimport, though.

<h1>Managed installs and managed uninstalls</h1>
1. Using MunkiAdmin, take Firefox out of the optional installs for the site_default
manifest.
2. Put it in the managed installs for the site_default manifest.
3. Then, in your VM, launch up Managed Software Center and check again for updates. If
Firefox isn't installed, it should install.
4. In your VM, delete Firefox, and check again for updates in Managed Software Center,
and you should see Munki wants to reinstall Firefox. That's because Munki is a "desired
state" configuration management tool. If Firefox is a managed install, that means "the
desired state is Firefox is installed." So if you delete Firefox, Munki will desire to
reinstall Firefox.
5. In MunkiAdmin, take Firefox out of the managed installs and put it in the managed
uninstalls.
6. In your VM, check again for updates in MSC, and you should see Firefox gets deleted.
<h1>Importing new items into the Munki repo</h1>
Try downloading Atom, BBEdit, Slack, and Google Chrome, and importing each into the Munki
repo.
Once each item is downloaded, go to the terminal and type munkii and hit Tab. After you hit
Tab, that should autocomplete to munkiimport. Then drag to the terminal the .dmg you
downloaded.
The command will end up looking something like:
munkiimport /Users/username/Downloads/nameofapp.dmg
where username is your username, and nameofapp is the app you're importing into the Munki
repo.
Then, answer the questions during munkiimport and extract an app icon. Try adding some of
these apps to managed installs, managed uninstalls, optional installs, and see what happens
on your VM.
