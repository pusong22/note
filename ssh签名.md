# ssh签名

## 开启ssh-agent
```shell
env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add ~/.ssh/id_rsa_gmail
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add ~/.ssh/id_rsa_gmail
fi

unset env
```

## 配置
### 1. 将公钥添加到github中
### 2. 本地开启签名配置
1. git config --global gpg.format ssh
2. git config --global user.signingKey ~/.ssh/id_rsa
3. git config --global gpg.ssh.allowedSignersFile = ~/.ssh/allowed_signers
    >```shell
    > 文件内容格式：email + 公钥
    > ```
4. git config --global commit.gpgign true
5. git config --global tag.gpgsign true