---
layout: post
title:  "Setting up Munki in MacOS server"
date:   2021-09-023 11:58:57 -0700
categories: Munki MDM Tool
---
[Where to download Munki](https://github.com/munki/munki)

<img src="https://raw.githubusercontent.com/wiki/munki/munki/images/managed_software_center.png" alt="MSC" width="460" height="345">
	<head>
		<style>
		body {
			background-image: url('https://giphy.com/gifs/90s-80s-illustration-l0HlNaQ6gWfllcjDO/fullscreen');
			background-repeat: no-repeat;
			background-attachment: fixed;  
			background-size: cover;
			border-radius: 50px;
			margin-left: 120px;
			margin-right: 120px;
			font-family: arial, sans-serif;
		}	
		</style>
	</head>


<h1>Seeting up your inviroment</h1>
Munki can run on almost any web server, and macOS comes with Apache 2, so setting up a demonstration Munki server on any accessible Mac is a breeze. You can even run a Munki server and a Munki client on the same computer, which is what we'll do here. Munki will be installed on a macOS computer that does not have Server.app installed. To get started if you don’t have a second computer you can also use a vm for this example. 

<h1>Things needed to set up</h1>
1. Server machine Mac computer
2. Client machine (VM Mac OS or another Mac computer)
3. Munki installed in local computer

<h1>Building your Munki Repo Sever</h1>
Now construct a directory structure in /Users/Shared for the Munki "server" and then configure Apache2 to serve it over HTTP. The following steps may be completed in either Finder or Terminal, although it's easier to type them down as Terminal commands:

cd /Users/Shared/
mkdir munki_repo
mkdir munki_repo/catalogs
mkdir munki_repo/icons
mkdir munki_repo/manifests
mkdir munki_repo/pkgs
mkdir munki_repo/pkgsinfo

Next Apache 2 has to read and traverse all of these directories:
chmod -R a+rX munki_repo

The next step is to inform Apache2 to use HTTP to serve the munki repo directory. You could change the /etc/apache2/httpd.conf file, or any of Apache2's other.conf files.

sudo ln -s /Users/Shared/munki_repo /Library/WebServer/Documents/

This builds a symlink to the new munki repo directory within /Library/WebServer/Documents/. On macOS, the DocumentRoot for Apache 2 is set to /Library/WebServer/Documents/, which means it will serve anything in that directory over HTTP.

Now to turn on Apache 2:
sudo apachectl start

To reverse this change: 
sudo apachectl stop

The munki server is now working !

