---
layout: post
title:  "Blog-3-Munki-Import-Configuration"
date:   2021-09-28 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="https://www.techrepublic.com/a/hub/i/r/2018/11/21/a1010cf1-5bb8-4cb9-b89b-ca8db7594479/resize/1200x/6b354ad0745f0bd6902979de92f2ca05/201845figure-k.jpg" alt="MSC" width="460" height="345">



<h1>Importing application in to Munki</h1>
Munki can run on almost any web server, and since macOS uses Apache 2, it's quite simple to put up a sample Munki server on any accessible Mac. You can even run a Munki server and a Munki client on the same computer, which is what we'll do here. Munki will be installed on a macOS computer that does not have Server.app installed.

<h2>Creating a Repo</h2>
You have a functional Munki repo, however it is entirely empty and useless. Let's get started populating the repo. Munkiimport is the tool we'll use to import packages into the Munki repo. Till it can use it, we must configure it by instructing it where to access our repository, among several other things.
 
The location to the Munki repo is initially requested, and since we set one up at /Users/Shared/munki repo, we enter that with the file:/ prefix. This might generally be an afp:/ or smb:/ URL indicating the share if you were hosting a repo remotely.

After that, you'll be asked to choose an editor for the pkginfo files. You can use /usr/bin/vi, /usr/bin/emacs, or BBedit if you prefer command-line editors.

Now, let’s get a package to import. Google is a good example package, and you can download it from http://www.google.com/.
<p><b>
<dl>
<dt>bash-3.2$ /usr/local/munki/munkiimport ~/Downloads/Chrome\ 94.0.4606.71.dmg </dt>
           <dd>Item name: Chrome</dd> 
        <dd>Display name: Chrome</dd>
        <dd> Description: Web browser from Google</dd>
             <dd>Version: 94.0.4606.71</dd>
            <dd>Category: Internet</dd>
           <dd>Developer: Google</dd>
  <dd>Unattended install: False</dd>
<dd>Unattended uninstall: False</dd>
            <dd>Catalogs: testing </dd>   
<dt>Import this item? [y/n] y</dt>
<dt>Upload item to subdirectory path []: apps/google</dt>
<dt>Path /Users/Shared/munki_repo/pkgs/apps/google doesn't exist. Create it? [y/n] y</dt>
<dd>No existing product icon found.</dd>
<dt>Attempt to create a product icon? [y/n] y</dt>
<dd>Attempting to extract and upload icon...</dd>
<dt>Created icon: /Users/Shared/munki_repo/icons/Chrome.png</dt>
<dd>Copying Firefox 61.0.2.dmg to /Users/Shared/munki_repo/pkgs/apps/google/Chrome 94.0.4606.71.dmg...</dd>
<dt>Edit pkginfo before upload? [y/n]: y</dt>
<dd>Saving pkginfo to /Users/Shared/munki_repo/pkgsinfo/apps/google/Chrome 94.0.4606.71.dmg...</dd>
</dl>
</b></p>

Then, using the munki "munkiimport" tool, point it to the disk image we just downloaded.
If you want to import the item, write yes, and if there are any faults, type no.

 munkiimport copies the Google package to /Users/Shared/munki_repo/pkgs/apps/google and saves the pkginfo to /Users/Shared/munki_repo/pkgs/apps/google/Chrome 94.0.4606.71.dmg.

<dd>Rebuild catalogs? [y/n]</dd> 

Munki clients do not use particular pkginfo files to locate accessible software; instead, they obtain and review Munki catalogs. So, in order to use the pkginfo we just created, we'll need to rebuild all of the specified catalogs with new versions. Munkiimport rebuilds the Munki catalogs if you answer "yes" to this popup.

<dt>Rebuild catalogs? [y/n] y</dt>
<dd>Adding apps/mozilla/Firefox-61.0.2 to testing...</dd>

We notice a single piece has been uploaded to the testing catalog because our Munki repo only includes one package (and its accompanying pkginfo). We may go through our previous work one more. Go to http://localhost/munki repo/catalogs/testing in your browser. A property list should appear, containing the pkginfo for Chrome.

