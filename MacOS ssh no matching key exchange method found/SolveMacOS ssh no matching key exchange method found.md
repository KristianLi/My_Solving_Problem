# Solve:MacOS ssh no matching key exchange method found

较新的MacOS在连接一些采取旧的不安全的ssh交换密码协议的服务器时会报错无法连接，比如：

```bash
Unable to negotiate with xxxxxxx port xxxx: no matching key exchange method found. Their offer: diffie-he11man-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1
```



解决方法如下：

首先打开ssh的config文件进行编辑

```
sudo nano /etc/ssh/ssh_config
```

用方向键控制光标拉到文本末端，在文本末端写入以下代码

```bash
HostkeyAlgorithms +ssh-dss
PubkeyAcceptedKeyTypes +ssh-dss
KexAlgorithms +xxxxxxxxx(这里根据报错自行补充）
```



最后一行根据我们的需要进行添加，比如我这里的报错信息提到

```
Their offer: diffie-he11man-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1
```



那么我们就在最后一行写

```bash
KexAlgorithms +diffie-he11man-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1
```



然后根据下方提示可以control+X退出，然后按Y保存

最后重新在终端用ssh/fstp命令尝试连接服务器即可。