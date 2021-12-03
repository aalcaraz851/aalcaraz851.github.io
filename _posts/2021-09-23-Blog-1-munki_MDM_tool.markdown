---
layout: post
title:  "Blog-1-Setting up Munki in MacOS server"
date:   2021-09-23 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="http://www.amsys.co.uk/wp-content/uploads/munki-repo.jpg" alt="MSC" width="460" height="345">



<h1>Setting up your environment</h1>
Munki can run on almost any web server, and macOS comes with Apache 2, so setting up a demonstration Munki server on any accessible Mac is a breeze. You can even run a Munki server and a Munki client on the same computer, which is what we'll do here. Munki will be installed on a macOS computer that does not have Server.app installed. To get started if you don’t have a second computer you can also use a vm for this example. 

<h1>Things needed to set up</h1>
1. Server machine Mac computer
2. Client machine (VM Mac OS or another Mac computer)
3. Munki installed in local computer

<h1>Building your Munki Repo Sever</h1>
Now construct a directory structure in /Users/Shared for the Munki "server" and then configure Apache2 to serve it over HTTP. The following steps may be completed in either Finder or Terminal, although it's easier to type them down as Terminal commands:

<p>cd /Users/Shared/</p>
<p>mkdir munki_repo</p>
<p>mkdir munki_repo/catalogs</p>
<p>mkdir munki_repo/icons</p>
<p>mkdir munki_repo/manifests</p>
<p>mkdir munki_repo/pkgs</p>
<p>mkdir munki_repo/pkgsinfo</p>

<h3>Next Apache 2 has to read and traverse all of these directories:</h3>
chmod -R a+rX munki_repo

<h4>The next step is to inform Apache2 to use HTTP to serve the munki repo directory. You could change the /etc/apache2/httpd.conf file, or any of Apache2's other.conf files.</h4>

sudo ln -s /Users/Shared/munki_repo /Library/WebServer/Documents/

<h4>This builds a symlink to the new munki repo directory within /Library/WebServer/Documents/. On macOS, the DocumentRoot for Apache 2 is set to /Library/WebServer/Documents/, which means it will serve anything in that directory over HTTP.</h4>

<h4>Now to turn on Apache 2:</h4>
sudo apachectl start

<h4>To reverse this change: </h4>
sudo apachectl stop

<h4>127.0.0.1/munki_repo</h4>
The munki server is now working !

