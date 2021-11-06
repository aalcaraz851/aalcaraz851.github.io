---
layout: post
title:  "Blog-7-Munki-Creating custom packages"
date:   2021-11-05 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="http://www.amsys.co.uk/wp-content/uploads/munki-admin-packages-java.png" alt="MSC" width="460" height="345">



<h1>Creating custom packages</h1>
Normallly you can download premade pachages but you also can create your own
custom packages to deliver your own custom files and folders to client Macs.

A program to give you a visual aspect is called "Packages", thi sis a program to help undersatnd how to creata package for munki.

When you start it up, it'll ask if you want to create a Distribution package or a Raw Package.
A distribution package contains a bunch of raw packages, and that's probably not a good place
to start. So definitely select Raw Package.

For the Project Name, put in test custom package

/test custom package/ should appear in the Project Directory, indicating that the test custom package folder will be in your home folder. If you wish to include it,

Choose another location to save the project from your Desktop or Documents folder by clicking Choose. Click Create once you've decided on a place. The Project tab is the first. All of the defaults should be left alone.

The Settings tab is the next tab. A reverse URL is used as the Identifier. So, instead of testpackage.snap.com, the identifier for a package named testpackage will be testpackage.snap.com.

com.snap.testpackage.
Replace com.snap.testcustompackage with com.snap.testcustompackage in the identifier.


For the time being, the Version is 1.0, which is acceptable. You might wish to modify that to 1.1 (minor adjustment) or 2.0 when making later versions of the package (major change).

The Payload tab represents the principal function of a package, which is to transport files and/or folders to a client workstation. The payload is the transmitted file(s)/folder(s). Scroll down to the Users folder, and then choose the Shared folder within it for this experiment. To add a new payload file, click the Plus symbol beneath those folders. Any file on your PC might be the culprit. It may be a PDF or a script—any file you want delivered to the test system where this package will be installed.




Preinstall and postinstall scripts may be found on the Scripts tab. For the time being, we'll just provide a payload and leave those out.

First, save your project by going to File > Save. Then select Build > Build from the drop-down list.

If you close and reopen Packages, then try to Build > Build again, you can get the following error:
You don't have permission to create it inside the 'Shared' folder, thus you can't copy anything at whateverthepathis. To remedy this, exit Packages and go to System Preferences > Security & Privacy > Encryption. Check the box next to packages dispatcher by clicking the lock to make changes > Full Disk Access.





Relaunch Packages, then try to build again; Santa will most likely block a new Packages process, so upvote it. Relaunch Packages (all of the Santa/TCC work we've been doing to get Packages to work is a solid argument to use munkipkg instead, but Packages is still a fine place to start for custom packages). Now, go to Build > Build, and your package should be in /Users/username/test custom package/build/test custom package.pkg.

You can use Finder if you wish, but the Terminal is the fastest option to make a before-and-after comparison for installing the software. Copy and paste the following commands into a terminal window:

pkgutil --pkgs | grep com.snap.testcustompackage
ls -l /Users/Shared

Leave that terminal window open for now.

Double-click test custom package.pkg to install your package.

Then, open a new terminal window and run those same two commands:
pkgutil --pkgs | grep com.snap.testcustompackage
ls -l /Users/Shared

You should notice the receipt in the first command (which checks receipts), and your file should be delivered to /Users/Shared in the second step.

To utilize this package in your VM, use munkiimport to import it into your Munki repo and try it as an optional install (installing and removing via the VM client in Managed Software Center).