# THM-GitHappens
## Git Happens CTF 🏳️

### 1. Scan the network using NMap
>start by scanning the target with Nmap. We discover a web service running on standard port `80/tcp` 

 `PORT   STATE SERVICE VERSION
80/tcp open  http    nginx 1.14.0 (Ubuntu)
| http-git: 
|   10.10.113.201:80/.git/
|     Git repository found!
|_    Repository description: Unnamed repository; edit this file 'description' to name the...
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: Super Awesome Site!
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel`


### 2. Git repo
Nmap script also discovered a git repository, which we can confirm with gobuster:


### 3. Dump the git repo
Let’s use gitdumper from GitTools to download the content of the Git repo:

### 4. Git logs
Now, let’s check the logs. We can see several commits.

### 5. Show files
Based on these commits, we can use git show to highlight files modifications from the commits (we’ll start with the reverse order for the commits). For the initial commit with ID 2f423697bf81fe5956684f66fb6fc6596a1903cc, there is nothing interesting, but the second commit with ID 395e087334d613d5e423cdf8f7be27196a360459 reveals the source code of the page, where credentials appear in the clear:

### 6. Authenticate
Now that we have the credentials (admin:Th1s_1s_4_L0ng_4nd_S3cur3_P4ssw0rd!), we can use them against the authentication page (http://10.10.113.201). It redirects to http://10.10.113.201/dashboard.html with a message: Awesome! Use the password you input as the flag!


# FLAG CAPTURED 🥇
Flag: Th1s_1s_4_L0ng_4nd_S3cur3_P4ssw0rd!
