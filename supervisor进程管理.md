# Supervisor进程管理
Supervisor（Supervisor: A Process Control System）是用Python开发的一个client/server服务，是Linux/Unix系统下的一个进程管理工具，不支持Windows系统。
它可以很方便的监听、启动、停止、重启一个或多个进程。
用Supervisor管理的进程，当一个进程意外被杀死，supervisort监听到进程死后，会自动将它重新拉起，很方便的做到进程自动恢复的功能，不再需要自己写shell脚本来控制。

## supervisor安装完成后会生成三个执行程序:supervisortd、supervisorctl、echo_supervisord_conf
supervisortd：用于管理supervisor本身服务
supervisorctl：用于管理我们需要委托给superviso工具的服务
echo_supervisord_conf：用于生成superviso的配置文件
supervisor的守护进程服务(用于接收进程管理命令)
客户端(用于和守护进程通信,发送管理进程的指令)

## 服务器使用Supervisor
