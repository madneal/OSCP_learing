# OSCP learning

## 官方

* [官方考试说明](https://www.lshack.cn/wp-content/uploads/2019/02/lshack.cn_2019-02-12_09-29-54.pdf)
* [PWK FAQ](https://support.offensive-security.com/#!pwk-general-questions.md)
* [OSCP exam FAQ](https://support.offensive-security.com/oscp-faq/)
* [IRC](https://www.offensive-security.com/offsec-irc-guide/)

## 考试报名

## 资料链接

## cheetsheet 

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
  
