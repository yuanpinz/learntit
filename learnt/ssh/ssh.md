 

# SSH Notes

## 在服务器安装ssh-server

```bash
sudo apt-get install openssh-server
```

## 在客户端连接服务器

```bash
ssh <user>@<host> -p <port>
```

## 免密码登录

1. 在客户端生成SSH钥匙

   ```bash
   ssh-keygen
   ```

   公钥放在~/.ssh/id_rsa.pub

   私钥放在~/.ssh/id_rsa

2. 上传公钥到服务器

   ```bash
   ssh-copy-id <user>@<host> -p <port>
   ```

   或（若没有安装ssh-copy-id）

   ```bash
   ssh <user>@host -p <port> 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
   ```

## 配置别名

在~/.ssh/config中追加

```shell
Host <alias>
	HostName <host>
	User <user>
	Port <port>
```

然后可通过别名连接服务器

```bash
ssh <alias>
```

## 传输文件

```bash
scp -P <port> <local_path> <user>@<host>:<remote_path> # 上传本地文件
scp -P <port> <user>@<host>:<remote_path> <local_path> # 下载远程文件
```

配置别名后可用`<alias>`取代`<user>@<host>`且不需要`-P`参数

## 端口转发



## 传递图形界面

使用`-X`参数，调用X  Server传递图形界面

