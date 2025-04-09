# H2 Favorite color: purple

## [Assignments](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h2-lempivari-violetti)

#### x) [Read and answer the questions briefly.](#x)
- Explain the idea of ​​the pyramid of pain in 1-2 sentences. Bianco 2013: [Pyramid of Pain](http://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
- Explain the idea of ​​the Diamond Model in 1-2 sentences. Caltagirone et al 2013: [Diamond Model](https://www.threatintel.academy/wp-content/uploads/2020/07/diamond-model.pdf)

#### a) [Apache log.](#a) 
- Install the Apache web server on your local virtual machine. Surf to your server with an unencrypted HTTP connection, http://localhost . Find the log line corresponding to your own page load. Analyze one such log line, i.e. explain all its points. (If you are not very familiar with Apache, you can just install it for this task and test it with the default web page. So you don't need to make your own homepages etc.)

#### b) [Nmapped.](#b)
- Port scan your own web server using localhost and 'nmap -A'. Explain the results. (Just http port 80/tcp is enough)

#### c) [Scripts.](#c) 
- Which scripts were automatically enabled when you used the "-A" parameter? (Shown under open port numbers, http-blah, http-blöh...).

#### d) [Traces in the log.](#d) 
- Search the web server logs for traces of port scanning (NSE or Nmap Scripting Engine scripts in the scan). Can you find the word "nmap" in upper or lower case? Explain the matches. What searches or rules could you use to identify a port scan in some other log, if it is so extensive that you cannot read all the lines yourself?

#### e) [Wire sharking.](#e) 
- Capture network traffic while port scanning with Wireshark. Note that localhost uses the "Loopback adapter" or "lo". Save the pcap. Find the sections with the word "nmap" and comment them out. You don't need to analyze every section of every packet, a more general look is enough.

#### f) [Net grep.](#f) 
- Capture network traffic with the 'ngrep' command and display the entries containing the word "nmap".

#### g) [Agent.](#g) 
- Change nmap's user-agent so that it looks like a regular web browser.

#### h) [Smaller traces.](#h) 
- Port scan your web server again using localhost. Look at both the Apache log and the intercepted network traffic. What has changed when you changed the user-agent? Is the text string "nmap" still in the log?

#### i) [Slightly harder: LoWeR ChEcK.](#i) 
- Remove every last "nmap" text from the script scan. Search for the text you found in the /usr/share/nmap directory and replace it with another one. Do a port scan and check that "nmap" does not appear in uppercase or lowercase in the Apache log or in the intercepted network traffic. (In this task, you can directly edit the lua scripts under /usr/share/nmap, 'sudoedit'. So packaging the modified version is excluded from the task.)

#### j) [Optional, hard: Invisible, invincible.](#j) 
- Find another nmap script that has the string "nmap" in uppercase or lowercase in its network traffic. Change the nmap code so that the string is no longer visible in the network traffic.

## Answers

### [X.](#x-read-and-answer-the-questions-briefly)

#### Pyramid of pain:

![image-24](https://github.com/user-attachments/assets/803b69f6-ad5e-438b-a3e9-b57988599ba7)  
https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html

Illustrates the relative difficulty an attacker faces when changing different indicators to avoid detection. The higher an indicator is on the pyramid, the more disruptive it is for the attacker when a defender uses it for detection or response.

- **Hash Values** (bottom of the pyramid):  
Easy for an attacker to change. For example, adding random text to a file can generate a completely different hash.

- **TTPs – Tactics, Techniques, and Procedures** (top of the pyramid):  
Difficult for an attacker to modify. These represent behavioral patterns and strategic methods. When defenders are able to detect and respond to TTPs, it becomes significantly harder for attackers to operate without being caught.

#### Diamond Model

![image-25](https://github.com/user-attachments/assets/602be078-b93e-4af0-93b5-be2e57270ff2)  
https://www.linkedin.com/pulse/diamond-model-intrusion-analysis-overview-aman-agarwal

The Diamond Model illustrates how an attack is carried out. It can be used to analyze an attack.

### [A.](#a-apache-log)

Let's install apche2 with the command:   
`sudo apt install apche2`

In Kali Linux, Apache2 is already installed by default:

![image](https://github.com/user-attachments/assets/c1e386f6-3b60-44b7-a5ac-6d95928db860)

Now, start the Apache2 daemon with the command:  
`sudo systemctl start apache2`

Then, we can "surf" to our web server by going to: `http://localhost`

![image-1](https://github.com/user-attachments/assets/5ec09e3d-9691-44df-a50f-f1d3d766c5a1)

We can check the Apache2 logs in: `/var/log/apache2/`

![image-2](https://github.com/user-attachments/assets/1114d289-33a0-4d1d-840c-e90ccf196902)

Here’s an example of a request logged by Apache:

`127.0.0.1 - - [08/Apr/2025:08:39:40 -0400] "GET / HTTP/1.1" 200 23383 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"`

- `127.0.0.1` is the IP adress that the request came from
- `-` this is usually blank
- `-` this would show the username of the client **HTTPS authentication**
- `[08/Apr/2025:08:39:40 -0400]` this is the time when the request came from
- `GET / HTTP/1.1` this is the method and the **HTTP** version of request
- `200 23383` this shows the response status and the size that was returned to the client
- `-` this would show the page that referres to that link
- `Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0` this shows information about the useragent like Firefox version, linux type etc...

In this example, there are three requests:
1. A **GET** request to fetch the main HTML document.
2. A **GET** request to retrieve the Debian logo.
3. A **GET** request for **favicon.ico**, this returned a **404** (Not Found) error, meaning the file wasn’t found.

https://httpd.apache.org/docs/current/logs.html

### [B.](#b-nmapped)

We can port scan our own web server using the command:   
`sudo nmap -A localhost`

- The `-A` flag enables several features, including:
    - OS detection
    - Version detection
    - Script scanning
    - Traceroute

![image-3](https://github.com/user-attachments/assets/838c49b9-5b3e-41b3-a704-acf3a1306fa5)

From the scan results, we can see that:
- The server is running on port **80**
- It’s using **Apache2**
- The OS is **Debian-based**
- The Apache version is **2.4.63**

### [C.](#c-scripts)

The scripts that were automatically enabled:
- http-title
- http-server-header

![image-4](https://github.com/user-attachments/assets/7d7946d2-1fe5-4748-a86d-47ee5b4b810e)

### [D.](#d-traces-in-the-log)

When we run the Nmap scan, this is what the logs look like:

![image-5](https://github.com/user-attachments/assets/a2a22a4d-08ea-4a9e-ac0e-0832341c2ca4)

We can identify that an Nmap port scan took place by looking for a few indicators in the logs:
- ![image-6](https://github.com/user-attachments/assets/d37d36f6-49b0-4669-9af2-ec883e49f2b5) This entry shows a request that Nmap sends to test how the server responds to an arbitrary or unexpected input
- We can also look at the User-Agent string in the request

### [E.](#e-wire-sharking)

When scannin with `sudo nmap -A localhost` and examining the network traffic with **wireshark**

The first 2001 packets are port scans to determine which ports are open

![image-13](https://github.com/user-attachments/assets/b2293853-bcea-4fd5-9367-48f650cc755c)

Only one port (port 80) responded with **SYN, ACK** flags which means it's open

![image-15](https://github.com/user-attachments/assets/72b11a4e-af3d-4434-b79f-978d43f2cea5)

Here are all the packets that contain the word "nmap" in the frame:

![image-16](https://github.com/user-attachments/assets/601bbd9a-fa75-4595-875b-5ebd2bbda93a)

For example, we can see:
- **nmaplowercheck** nmap checks **404** response
- **GET /.git/HEAD** nmap checks if a Git repository exist
- The different **OPTIONS** requests: Nmap determines which methods are allowed (**GET**,**POST**,**DELETE**...)

### [F.](#f-net-grep)

Network traffic captured using **ngrep**, can be filtered to display only content containing the word "nmap" with the command:  
`sudo ngrep -d lo -i nmap` 

- The `-d` flag specifies the network interface; in this case, the loopback interface (**lo**) is used
- The `-i` flag enables case-insensitive matching for the keyword

![image-17](https://github.com/user-attachments/assets/510187a5-1f56-4261-b7e1-c69231cb507b)

### [G.](#g-agent)

Nmap's User-Agent can be changed with the following command:  
 `sudo nmap --script-args http.useragent="<useragent>" -A localhost`

### [H.](#h-smaller-traces)

To make it more convincing, you can grab a real User-Agent from this site: https://useragentstring.com/pages/useragentstring.php

![image-7](https://github.com/user-attachments/assets/4a58f4d7-3ca9-4a7a-a464-fd03ae74c63c)

Now, if we run the scan again:

![image-8](https://github.com/user-attachments/assets/01d76526-eeed-4a4e-9ddb-907db7759d97)

![image-9](https://github.com/user-attachments/assets/ee1017a4-2633-488c-9b49-e2b1063ac3aa)

We can see that the User-Agent in the logs makes it look like the request came from a Windows machine running Firefox

### [I.](#i-slightly-harder-lower-check)

The **nmaplowercheck** is used by Nmap to test how the server handles **404 (Not Found)** responses

We can disable this check by editing the `http.lua` file located at:  
`/usr/share/nmap/nselib`

In there is this section on lines **2624-2627** 

![image-10](https://github.com/user-attachments/assets/c79bd2dd-0de9-45be-b999-dd5d05696a61)

To disable the check, simply comment out line **2625** like this:

![image-11](https://github.com/user-attachments/assets/dcdf8eb9-634d-40ee-a279-2ae86930dcab)

After saving the file, Nmap should skip the nmaplowercheck

Let’s run the scan again

Now, if we check the Apache2 logs:

![image-12](https://github.com/user-attachments/assets/ecb18379-44f9-4b16-9e43-4294c7031d3e)

There’s no mention of Nmap

### [J.](#j-optional-hard-invisible-invincible)

The script **http-vuln-cve2012-1823.nse** contains the word "nmap"

![image-18](https://github.com/user-attachments/assets/625bfa82-9761-4eff-8d6c-83bf7b0e5e4c)

![image-19](https://github.com/user-attachments/assets/f3a9f609-90b4-4826-8f90-1acd2a953fc5)

We can edit the script to echo something else

![image-20](https://github.com/user-attachments/assets/02804e24-bb42-4194-a7ba-976383606fb2)

We need to edit the highlighted strings

![image-21](https://github.com/user-attachments/assets/2b8825a5-d673-497f-9e0b-118582e88bc2)

Now, when we run the scan again, there should be no mention of "nmap"

![image-22](https://github.com/user-attachments/assets/83daec55-2325-46f5-ac48-73c138ece2bd)

![image-23](https://github.com/user-attachments/assets/5ec22057-af1b-4863-be28-fa2a37bfc1cb)

### Sources
- ngrep: https://linux.die.net/man/8/ngrep

- nmap: https://linux.die.net/man/1/nmap

- Picture of the Pyramid of Pain: https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html

- Picture of the Diamond model: https://www.linkedin.com/pulse/diamond-model-intrusion-analysis-overview-aman-agarwal

- User Agent String: https://useragentstring.com/pages/useragentstring.php

- Apache logs info: https://httpd.apache.org/docs/current/logs.html
