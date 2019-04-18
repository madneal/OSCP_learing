# Windows

## List services

`wmic service where started=true get name, startname`

# Linux

## Get remote script and execute

`bash <(curl -s http://mywebsite.com/myscript.txt)`

## ssh

### 使用 private key 登录

![AxtqoR.png](https://s2.ax1x.com/2019/04/16/AxtqoR.png)

修改 private key 权限，`chmod 4000`
