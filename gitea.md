# Docker 配置Gitea
使用Docker Compose来管理Gitea+MySQL
```shell
name: gitea # version过时了 

networks: # 配置一个全局网络
  gitea:
    external: false # build时创建

services:
  server:
    image: gitea/gitea:latest
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=1000
      - GITEA_database_DB_TYPE=mysql
      - GITEA_database_HOST=db:3306
      - GITEA_database_NAME=gitea
      - GITEA_database_USER=gitea
      - GITEA_database_PASSWD=gitea
    restart: always
    networks:
      - gitea
    volumes: # 映射
      - ./gitea:/data
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "8080:3000"
      - "2221:22"
    depends_on:
      - db


  db:
    image: mysql:8
    restart: always
    networks:
      - gitea
    volumes:
      - ./mysql:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=gitea
      - MYSQL_USER=gitea
      - MYSQL_PASSWORD=gitea
      - MYSQL_DATABASE=gitea


  #runner:
    #image: gitea/act_runner:latest
    #environment:
      #CONFIG_FILE: /config.yaml
      #GITEA_INSTANCE_URL: "http://192.168.2.196:8080"
      #GITEA_RUNNER_REGISTRATION_TOKEN: #"WwamWK9iqyMnlokVtexhNysR9YdwisKVxGh6LTBG"
    #restart: always
    #networks:
      #- gitea
    #volumes:
      #- ./config.yaml:/config.yaml
      #- ./data:/data
      #- /var/run/docker.sock:/var/run/docker.sock
    #depends_on:
      #- server


```

然后运行```docker compose up -d```，进行images的build和容器的创建以及启动。

## NOTES
在浏览器中初始化gitea配置时数据库信息要与yml中的一致，尤其时数据库主机的信息要于```GITEA_database_HOST```一致