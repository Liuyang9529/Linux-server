# Linux Crontab 定时任务

## crontab的使用
```
crontab [-u username]　　　　//省略用户表表示操作当前用户的crontab
    -e      (编辑工作表)
    -l      (列出工作表里的命令)
    -r      (删除工作作)
```

## crontab的命令构成为 时间+动作，其时间有分、时、日、月、周五种
```
操作符有：
    * 取值范围内的所有数字
    / 每过多少个数字
    - 从X到Z
    ，散列数字
```


## 实例1：在上午8点到11点的第3和第15分钟执行
```
3,15 8-11 * * * myCommand
```


## 服务器重启：
```
1、首先su root，到root环境下。

2、密码：Ligroup#220706

3、crontab -e 
#查看所有定时任务
50 11 1-7 * * /etc/rebootMondayOfFirstweekOfEachMouth

#/etc/rebootMondayOfFirstweekOfEachMouth内容：判断是否是周一，后面是重启
#!/bin/bash
[ "$(date '+%u')" = "1" ] && (/sbin/shutdown -r +10 "服务器10分钟后重启，请各位备份信息。")
```
