---
layout: post
title:  "Blog-6-Munki-Packages"
date:   2021-10-29 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="http://www.amsys.co.uk/wp-content/uploads/munki-admin-packages-java.png" alt="MSC" width="460" height="345">



<h1>Packages </h1>

Packages different from disk images
So far, we have been adding items to the repo that are disk images (.dmg) that contain an app
bundle (.app) that you'd ordinarily drag and drop to the /Applications folder, but Munki takes
care of for you but Munki also can deploy packages. Packages are a bit more complicated than disk images.
Packages can deliver several payloads (copy files to various locations). They can also run
scripts and packages leave receipts.

<h3>Import a package</h3>

Go to https://github.com/homebysix/docklib/releases/latest and download the latest docklib
.pkg (at the time of this writing, it's docklib-1.3.0.pkg).
Just as you did with the previous downloads, use munkiimport to import the .pkg you
downloaded. 
<h1>Package receipts</h1>
A Munki receipt is a lot like a real receipt in that it shows at one point something happened, but it isn't the thing that happened.
Receipts on macOS are quite similar—all they do is say "At some point, you installed this
package." You can completely delete the package's contents, and the receipt will still be there saying "At some point, you installed this."
By default, Munki will just use receipts to determine if a package is installed.
You can see all the package receipts on your Mac by running pkgutil --pkgs
You can narrow that down a bit by using grep: 

<h3>pkgutil --pkgs | grep munki</h3>

Then you can get even more detail by running pkgutil 

<h3>--pkg-info com.googlecode.munki.app </h3>

to see when the package was installed and what version was installed in MunkiAdmin, add docklib as a managed install to the common_software manifest. In your client device, go ahead and run
 
 <h3>sudo managedsoftwareupdate -vvv --checkonly </h3>

and you should see that Munki is deciding to install docklib based on the absence of the receipt. Once you install docklib using Managed Software Center, run 

<h3>sudo managedsoftwareupdate -vvv --checkonly </h3>

again, and you should see Munki considers docklib installed based on the presence of the receipt.

