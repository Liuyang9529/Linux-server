# 几个Server下载文件的问题

如果server出现问题，则可以从以下角度来考虑问题：

172服务器的路径：/home/web/public/htdocs/projects/PremPS/prj-sunddg/static/PDB_model/



以PremPS为例，运行server计算的脚本如下所示：
```
/usr/local/bin/python change_1.py 2023111405102320979361759 >2023111405102320979361759/change_debug.txt 2>&1
echo start:`date +"%Y-%m-%d %H:%M:%S"` >> ./2023111405102320979361759/time.log
python PremPS.py -i 2023111405102320979361759 >2023111405102320979361759/debug.txt 2>&1
/home/webservice/anaconda2/bin/python cut_vmd.py 2023111405102320979361759

**echo end:`date +"%Y-%m-%d %H:%M:%S"` >> ./2023111405102320979361759/time.log**

/home/webservice/anaconda2/bin/python transfer_PDB_info_cut.py 2023111405102320979361759 >arpeggio/file_space/2023111405102320979361759/transfer_debug.txt 2>&1
/usr/local/bin/python CollectResultsAndEmail.py 2023111405102320979361759
```

**出问题，可能是前端或者后端出问题**

可以通过查看./2023111405102320979361759/time.log，如果文件中start和end的时间都有，则是前端出问题，否则是后端出问题。

**（1）后端问题**

如：ddg值无法计算等

需要在153服务器上debug

先su premps 再输入密码web2017

cd /data/webservice/premps/

找到对应的jobid，查看里面的debug文件

**（2）前端问题**

则是172服务器上出问题。

前端问题，通过查看arpeggio/file_space/2023111405102320979361759/transfer_debug.txt文件，
来了解问题是什么。


注意：每次修改172服务器密码时，都需要修改每个server中transfer_PDB_info_cut.py
的hostname、username和password三个。

目前172的账户密码是：
```
hostname='10.20.212.172'

username='web'

password='qazxsw123'
```


需要修改的服务器及文件：
premps

prempdi

prempri          transfer_PDB_info.py

mutabind2

prempri


----------------------------------------------------------------------------------------------------------------

# 如果想本地运行一下jobid的mutabind，或者其他server

```
su root

Ligroup#220706

su mutabind

```

再去找哪一个哪一行没运行，直接运行即可。

----------------------------------------------------------------------------------------------------------------

# 设置了一个检查数据库能否连接的程序

```
def SEND(s):
    my_sender='925201392@qq.com'    # 发件人邮箱账号
    my_pass = 'yizvpdduyjrrbbhj'              # 发件人邮箱密码
    my_user=['20234221090@stu.suda.edu.cn']#,'minghui.li.2016@outlook.com']

    msg=MIMEText(s,'plain','utf-8')
    msg['From']=formataddr(["From liuyang",my_sender])
    msg['To']=formataddr(["Server Problem:",', '.join(my_user)])
    msg['Subject']="There may be a problem with Mutabind2!"

    server=smtplib.SMTP_SSL("smtp.qq.com", 465)
    login = server.login(my_sender, my_pass)
    assert login[1]==b'Authentication successful','login failed!'

    server.sendmail(my_sender,my_user,msg.as_string())
    server.quit()
```

在mutabind2的CollectResultsAndEmail.py中有连接数据库的try，except

设置如果数据库连接不成功，则给老师和我发邮件。










