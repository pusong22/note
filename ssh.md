# ssh配置

## 一些命令参数
- -T 不进行shell交互，常用于执行命令在进行登录时，执行完就自动退出。
- -t 进行shell交互。
- -i 指定密钥文件路径

## 端口转发
1. 远程端口转发  
把目标机的流量转发到本地  
    ```shell
    ssh -R remote(ip:port):local(ip:port) user@remote_address -p port
    ```

2. 本地端口转发  
    把本机的流量转发到目标机，常用来访问内网中的机器。  
    比如：某公司有一个内网机器A，不能访问外网；同时有一个机器B可以访问外网并且和A是在同一个局域网；现在有一个机器C就可以通过B来访问A。
    ```shell
    ssh -L C(ip:port):A(ip:port) user@B_address
    ```

