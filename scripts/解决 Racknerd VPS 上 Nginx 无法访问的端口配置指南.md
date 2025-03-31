# 解决 Racknerd VPS 上 Nginx 无法访问的端口配置指南

在使用 Racknerd 海外 VPS 搭建网站时，很多用户会遇到 Nginx 安装后无法通过外网访问的问题。本文将详细介绍如何通过防火墙配置开放 80/443 端口，确保网站正常访问。

## 问题排查步骤

### 1. 验证 Nginx 是否正常运行
首先需要确认 Nginx 服务是否已成功安装并运行：

bash
$ wget http://127.0.0.1
--2025-01-03 20:11:34--  http://127.0.0.1/
正在连接 127.0.0.1:80... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：615 [text/html]
正在保存至: "index.html"
2025-01-03 20:11:34 (83.5 MB/s) - 已保存 "index.html" [615/615])

👉 [【点击查看】2025年最新 Racknerd 优惠码及特价云服务器方案汇总](https://bit.ly/Rack_Nerd)

### 2. 检查端口开放状态
使用以下命令检查 80 和 443 端口是否开放：

bash
$ firewall-cmd --query-port=80/tcp
output: no
$ firewall-cmd --query-port=443/tcp
output: no

### 3. 开放防火墙端口
通过 firewall-cmd 命令永久开放 HTTP/HTTPS 端口：

bash
$ firewall-cmd --permanent --add-port=80/tcp
output: success
$ firewall-cmd --permanent --add-port=443/tcp
output: success

### 4. 重启防火墙使配置生效
修改配置后必须重启防火墙：

bash
$ firewall-cmd --reload
output: success

## 防火墙常用命令大全

掌握这些命令可以帮助您更好地管理 VPS 防火墙：

- **查看防火墙服务状态**
bash
$ systemctl status firewalld

- **查看防火墙运行状态**
bash
$ firewall-cmd --state

- **查看所有防火墙规则**
bash
$ firewall-cmd --list-all

- **查询特定端口状态**
bash
$ firewall-cmd --query-port=19999/tcp

- **开放/关闭端口**
bash
# 开放端口
$ firewall-cmd --permanent --add-port=80/tcp

# 关闭端口
$ firewall-cmd --permanent --remove-port=80/tcp

- **重启防火墙**
bash
$ firewall-cmd --reload

通过以上步骤，您应该已经成功解决了 Racknerd VPS 上 Nginx 无法通过外网访问的问题。合理配置防火墙是保障服务器安全的重要环节，建议只开放必要的服务端口。