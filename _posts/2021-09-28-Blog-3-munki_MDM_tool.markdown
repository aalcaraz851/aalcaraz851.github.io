---
layout: post
title:  "Blog-2-Munki-Client-Configuration"
date:   2021-09-28 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="hhttps://www.techrepublic.com/a/hub/i/r/2018/11/21/a1010cf1-5bb8-4cb9-b89b-ca8db7594479/resize/1200x/6b354ad0745f0bd6902979de92f2ca05/201845figure-k.jpg" alt="MSC" width="460" height="345">



<h1>Importing application in to Munki</h1>
Since Munki can use virtually any web server as its server, and since macOS ships with Apache 2, it’s very easy to set up a demonstration Munki server on any available Mac. You can even set up a Munki server on a single machine that is also a Munki client, and that is what we'll do here. We will set up Munki on a machine running macOS without Server.app installed.

<h2>Creating a repo</h2>
We now have a working Munki repo – but it’s completely empty and not useful at all. So let’s start to populate the repo.

The tool we will use to import packages into the munki repo is called munkiimport. We need to configure it before we can use it – telling it where to find our repo, among other things.
 

We are first asked for the path to the Munki repo, and since we set one up at /Users/Shared/munki_repo, that’s what we enter with the file:// prefix. If you were hosting a repo remotely, this would typically be an afp:// or smb:// URL specifying the share.

Next, you are asked for an editor to use for the pkginfo files. If you like command-line editors, you can specify /usr/bin/vi or /usr/bin/emacs or BBedit.

Next, let’s get a package to import. Google is a good example package, and you can download it from http://www.google.com/.

bash-3.2$ /usr/local/munki/munkiimport ~/Downloads/Chrome\ 94.0.4606.71.dmg 
           Item name: Chrome 
        Display name: Chrome
         Description: Web browser from Google
             Version: 94.0.4606.71
            Category: Internet
           Developer: Google
  Unattended install: False
Unattended uninstall: False
            Catalogs: testing    
Import this item? [y/n] y
Upload item to subdirectory path []: apps/google
Path /Users/Shared/munki_repo/pkgs/apps/google doesn't exist. Create it? [y/n] y
No existing product icon found.
Attempt to create a product icon? [y/n] y
Attempting to extract and upload icon...
Created icon: /Users/Shared/munki_repo/icons/Chrome.png
Copying Firefox 61.0.2.dmg to /Users/Shared/munki_repo/pkgs/apps/google/Chrome 94.0.4606.71.dmg...
Edit pkginfo before upload? [y/n]: y
Saving pkginfo to /Users/Shared/munki_repo/pkgsinfo/apps/google/Chrome 94.0.4606.71.dmg...


Next run the munki "munkiimport" tool and provide it a path to our downloaded disk image.

"munkiimport" will ask for if you want to import the item and if ther are any mistakes type no. 
 
 

 munkiimport copies the Google package to /Users/Shared/munki_repo/pkgs/apps/google and saves the pkginfo to /Users/Shared/munki_repo/pkgs/apps/google/Chrome 94.0.4606.71.dmg.

Rebuild catalogs? [y/n] 

Munki clients don’t use the individual pkginfo files; instead they download and consult Munki catalogs to find available software. So to actually make use of the pkginfo we just generated, we need to build new versions of all the defined catalogs. Answering “y” to this prompt causes munkiimport to rebuild the Munki catalogs.

Rebuild catalogs? [y/n] y
Adding apps/mozilla/Firefox-61.0.2 to testing...

Since we only have one package (and its corresponding pkginfo) in our Munki repo, we see a single item has been added to the testing catalog. Again we can check our work so far. In your web browser, navigate to http://localhost/munki_repo/catalogs/testing. You should see a property list which contains the pkginfo for Chrome.

