# docker拉入新用户

通过yaml文件安装，是安装对应的python环境

通过docker，是安装别人的linux环境

## 命令

(1) 首先需要su到root用户下

```
su root
```

输入密码

(2) 查看是否有docker组

```
sudo groupadd docker
```

(3) 添加新用户

```
usermod -aG docker liuyang
```

(4) 使组成员关系立即生效

```
su - liuyang
```

(5) 查看docker组里有哪些用户

```
getent group docker
```




