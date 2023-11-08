# 检查server的运行情况
在每次172服务器启动之后，都要启动5个server服务器

设置了自动启动
cat  /etc/rc.local

## 检查server的work情况
```
ps -ef | grep -i prempdi | wc -l
ps -ef | grep -i premps | wc -l
ps -ef | grep -i prempri | wc -l

#ps -ef | grep -i prempli | wc -l
#这个pli的在mutabind中的/home/web/wenyuhao/sunddg/uwsgi.ini


ps -ef | grep -i mutabind | grep /home/web/wenyuhao/sunddg/uwsgi.ini |wc -l

ps -ef | grep -i mutabind | grep /home/web/public/htdocs/projects/mutabind/index.fcgi |wc -l
```

如果结果不是1，则表示在运行。

## 关闭server
```
ps -ef | grep -i prempdi | awk '{print $2}' | xargs kill -9
```


## 操作步骤
我们需要添加一个检查程序，如果server不在work，则运行cat  /etc/rc.local中的server.sh

（1）
以prempdi为例
```
#!/bin/bash
while true
do
a=`ps -ef | grep -i prempdi | wc -l`
if [ "$a" = "1" ]; then
/etc/rc.d/init.d/runPremPDI.sh
else 
break
fi
done

```

(2)写完之后，我们使用chmod 777 *.sh

(3)最后使用vim写入/etc/rc.local文件中

即可完成自动启动的过程。







