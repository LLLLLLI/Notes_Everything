# SSH
通过跳板机A连接局域网内的服务器B时，常规的方法为先ssh到A，然后在A上ssh到B。这样会无法使用VSCode ssh或者Jupyter等调试工具，解决办法是配置ssh的配置文件，使本机能够直接ssh到局域网内的服务器  
编辑.ssh/config文件  
对于Windows用户，文件位置为`C:\Users\YourName\.ssh\config`  
对于Mac OS/Linux用户，文件位置为`~/.ssh/config`

配置文件内容如下([Reference](http://sshmenu.sourceforge.net/articles/transparent-mulithop.html))
```shell
Host A
    HostName a.a.a.a    # IP
    User user
    Port xxxx

Host B
    HostName b.b.b.b
    User user
    # for Mac OS/Linux
    ProxyCommand ssh -q A nc -q0 %h 22
    # for Window
    ProxyCommed  C:\Windows\System32\OpenSSH\ssh.exe -q A nc -q0 %h 22
```
此时若要登录跳板机A，可直接使用命令
```shell
ssh A
```
若要登录服务器B，可直接使用命令
```shell
ssh B
```
## 使用VSCode
安装Remote-ssh插件后按照上述配置即可
## 使用Jupyter
在服务器端启动jupyter
```
jupyter notebook --no-browser --port=8889
```
在本机连接服务器并配置端口映射
```
ssh -N -f -L localhost:8888:localhost:8889 B
```
`-N` 表示没有命令要被远程执行  
`-f` 表示在后台运行
此时在浏览器输入locahost:8888即可