# Debian 安装Docker

## 卸载包
```shell
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

## 使用APT进行安装
1. 配置docker的apt库
    ```shell
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    # Add the repository to Apt sources:
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/debian \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    ```

2. 安装所需要的包
    ```shell
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

3. 验证是否安装成功
    ```shell
    sudo docker run hello-world
    ```
    安装成功会打印一些信息

## 安装后续  
### 普通用户运行Docker
1. 创建docker用户组
    ```shell
    sudo groupadd docker

    ```
2. 添加用户到docker组中
    ```shell
    sudo usermod -aG docker $USER
    ```
3. 注销后登录
4. 验证是否成功
    ```shell
    docker run hello-world
    ```
### 在系统启动时启动docker
```shell
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```


## 一些命令
### docker compose
1. up = build + create + start
2. down = stop + remove
3. start/stop 开启/停止服务
4. build 对yml文件进行构建
5. create/rm 构建的image创建container/删除container
6. pull 获取最新的Images
7. ps 查看container
8. exec 进入运行的container中
9. run 运行一次