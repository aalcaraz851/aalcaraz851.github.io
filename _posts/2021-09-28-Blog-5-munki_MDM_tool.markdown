---
layout: post
title:  "Blog-5-Munki"
date:   2021-10-22 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="https://www.alansiu.net/munkiguide/wp-content/uploads/2019/01/munkiadmin05.png" alt="MSC" width="460" height="345">



<h1>What is the Included Manifest option in Munki?</h1>
You can launch Munki objects to two or more manifests without keeping them 
identical by using an included manifest.

Make a new manifest called Test software in MunkiAdmin. Keep catalogs blank and include Test software as an included manifest in site default. Next, in Test software's Optional Installs, Managed Installs, and Managed Uninstalls, create an item.

Optional Installs: This option will give the user to option install a program from Manager Soft Center

Managed Installs:  This will install the program into the users computer in the background, unlike the optional install this will not show in Manager Soft Center.

Managed Uninstalls: This Unistalls a program from a user with out prompt them. In the backgreound this will unistalla promblem such as an out of date program, this does the opposite of the Managed Install.

 Once you apply one of these three options run
 sudo managedsoftwareupdate -vvv --checkonly 
 output instead of using Managed Software Center.

<h3>Munki Logs </h3>

Munki has logs to look into when running installs, munki import or anything you would see if an error comes up. In the command line run on the client device :

managedsoftwareupdate -vvv --checkonly

To see these logs, open Managed Software Center and then press Cmd-L while the program is open and another way find the actual logs if you go to 
Finder > Go > Go to Folder
 you can enter a file path.

 In the client device the it would be in 
 /Library/Managed Installs/Logs/ManagedSoftwareUpdate.log

 From the Mac Host you can find it here:
 /var/log/ManagedSoftwareUpdate.log

Depending on your company these logs can be ina different location, this feature is very usefull because if there is an unistall loop or an error with an installtion or and issue with Managed Software Center. Logs are  importing so they keep track of any issue.