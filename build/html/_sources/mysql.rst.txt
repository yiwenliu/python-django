windows安装mysql
===================
下载
------
从官网上下载太慢，从一个镜像下载的，https://mirrors.tuna.tsinghua.edu.cn/mysql/downloads/

安装
------
运行下载的msi文件时，并没有像以前的版本一样提供配置root密码，服务端口的窗口。

配置
--------
运行完msi文件后，要运行mysql时一堆错误，记录详细过程如下。

1. 把bin（ C:\Program Files\MySQL\MySQL Server 8.0\bin）添加到path
2. 用“管理员权限”打开cmd，然后一定要进入mysql的bin目录，执行下列命令。

.. note::
	否则，windows可能错误地指定mysqld所在的目录，导致>net start mysql运行失败

3. > mysqld --initialize

.. note::
	这个命令会在C:\Program Files\MySQL\MySQL Server 8.0\目录下创建data文件夹

4. > mysqld --install

.. note::
	这个命令会把mysql安装成windows服务，服务名采用默认的MySQL

5. > net start MySQL

修改root密码
---------------
安装时，会生成一个随机的root密码，需要修改。

参考链接：https://blog.csdn.net/baidu_32363401/article/details/81544573

1. 采用上述链接中的“方案二”，就修改好了root密码。
2. 关闭“方案二”中以非服务方式启动的mysqld

.. note::
	>mysqladmin -u root -p shutdown
	Enter password: xxx（用新改的密码即可）

Q&A
-----
1. 删除mysql服务
^^^^^^^^^^^^^^^^^^^
https://dev.mysql.com/doc/refman/8.0/en/windows-start-service.html中“Removing the service”小节。

.. note::
	如果用命令行没有删除干净，就得去删除注册表了，见下一个Q&A

2. 修改windows服务的参数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. note::
	如果没有在Mysql bin目录下执行>mysqld install，就容易出现mysql服务中mysqld路径参数错误

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services中的ImagePath字段

3. 查询错误
^^^^^^^^^^^^^
> mysqld --console