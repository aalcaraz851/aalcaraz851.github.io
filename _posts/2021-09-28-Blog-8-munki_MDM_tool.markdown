---
layout: post
title:  "Blog-8-Gorilla"
date:   2021-11-12 11:58:57 -0700
categories: Munki MDM Tool
---

<img src="https://github.com/1dustindavis/gorilla/blob/main/gorilla.png" alt="MSC" width="460" height="345">



<h1>What is Gorilla?</h1>
Gorilla is intened to to provide application managenment on Windows similiar to Munki applications.

<h1>How to get Started</h1>
Setting up the web server to host at least one catalog, manifest, and packages. The structure should look like :

[web root]

├── manifests

│   ├── *.yaml

├── catalogs

│   ├── *.yaml

└── packages

    ├── *.nupkg

    ├── *.msi

    ├── *.exe

    └── *.ps1

Next is setting up the Windows Client, the client will have to download "gorilla binary" and "Client Configuration".

Download gorilla binary: https://github.com/1dustindavis/gorilla/releases

<h1>Client Configuration Set Up:</h1> 
The configuration file is in yaml format and is located at 
%ProgramData%/gorilla/config.yaml
 by default, but it may also be given as follows: gorilla.exe -config path to config.

 an exmaple file:
 ---
url: https://YourWebServer/gorilla/
manifest: example
catalogs: 

  - alpha

  - beta

app_data_path: C:/gorilla/cache

auth_user: GorillaRepoUser

auth_pass: pizzaisyummy

tls_auth: true

tls_client_cert: c:/certs/client.pem

tls_client_key: c:/certs/client.key

tls_server_cert: c:/certs/server.pem

<h3>Required Keys</h3>
The path on your server that contains the folders for global manifests, catalogs, and packages is specified by url. (You may utilize a local file repository by supplying a "file:" / protocol: "url: C:/example/gorilla/local/)"
The primary manifest associated to this computer is manifest.

<h3>Optional Keys</h3>
"catalogs" is an array of catalogs that are assigned to this machine. If you do not provide a catalog in the config, you must have one in a manifest.

"app_data_path" is Gorilla's working directory, and may store copies of manifests, catalogs, or packages. If 

"app_data_path" is not provided, it will default to %ProgramData%/gorilla/.

"url_packages" is an optional base url to be used instead of url when downloading packages.


<h4>Basic Auth</h4>
"auth_user" is an optional username for http basic auth.

"auth_pass" is an option password for http basic auth.

<h4>TLS Auth</h4>

"tls_auth" must be true if you are using TLS mutual authentication.

"tls_client_cert" is the absolute path to your client certificate in PEM format.

"tls_client_key" is the absolute path to your client private key in PEM format.

"tls_server_cert" is the absolute path to your server's CA cert in PEM format.

<h1>Running Gorilla</h1>
Gorilla will have to run as the administrator. It would most likely be launched as a scheduled process or service in production, but you can try it by opening a PowerShell or CMD window as an administrator and running C:pathtogorilla.exe.

Run gorilla.exe -help to see a list of possible arguments and a help message.

C:ProgramDatagorillagorilla.log is where logs are saved.


