
Automated discovery is the process of using tools to discover content rather than doing it manually. This process is automated as it usually contains hundreds, thousands or even millions of requests to a web server. These requests check whether a file or directory exists on a website, giving us access to resources we didn't previously know existed. This process is made possible by using a resource called wordlists.

**What are wordlists?**

Wordlists are just text files that contain a long list of commonly used words; they can cover many different use cases. 
[https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) 

  

**Automation Tools**
**ffuf:**
```shell-session
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://MACHINE_IP/FUZZ
```

**dirb:**
```shell-session
user@machine$ dirb http://MACHINE_IP/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

**gobuster:**
```shell-session
user@machine$ gobuster dir --url http://MACHINE_IP/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```
