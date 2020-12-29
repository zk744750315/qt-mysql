# qt-mysql
关于qy  mysql 创建数据库  以及打包生成exe文件后会报错：driver not loaded的问题
安装了MySQL  qt以后，因为qt是没有mysql的驱动文件的，需要在qt的编译器如  msvc32、msvc64、minGW32、minGW64的bin文件夹下面添加libmysql.dll、libmysql.lib文件，这些文件在mysql文件夹里面：
我的电脑中的位置：C:\Program Files\MySQL\MySQL Server 5.5\lib\     
注意：mysql是32位的，对应的libmysql.dll、libmysql.lib文件也是32位的，需要放在msvc32、minGW32、的bin文件夹下，假如mysql是64位的，对应的libmysql.dll、libmysql.lib文件就是64位的，需要放在msvc64、minGW64、的bin文件夹下，
完成以上操作，qt就可以操作mysql数据库了


但是在完成qt工程，生成release文件后，需要将生成的工程文件打包成可以运行的exe文件方法如下：
详见：https://blog.csdn.net/qq_39054069/article/details/96481902
此处我们的工程是用用64位的minGW创建的；
打开关于release相关的文件夹，找到该目录下release目录下的.exe程序。此时你点击是运行不成功的。因为缺少QT必要的库文件。将这个.exe文件拷贝出来，创建一个空的文件夹，比如warehouse，放在这个文件夹下。比如exe文件全名：Warehouse.exe,位置：E:\word\build-Warehouse-Desktop_Qt_5_12_3_MinGW_64_bit-Release\release\warehouse
然后打开minGW64的命令提示符，（可以cortana搜索qt,在弹出的结果中直接打开即可）
然后进入E:\word\build-Warehouse-Desktop_Qt_5_12_3_MinGW_64_bit-Release\release\warehouse文件夹，方法：输入cd /d E:\word\build-Warehouse-Desktop_Qt_5_12_3_MinGW_64_bit-Release\release\warehouse
然后执行打包命令 ，方法：输入如下命令行：windeployqt 程序名 敲击回车。（此处为:windeployqt Warehouse.exe）
最后E:\word\build-Warehouse-Desktop_Qt_5_12_3_MinGW_64_bit-Release\release\warehouse这个文件夹就是最终的程序文件，正常情况下是可以双击exe文件直接运行的，但是因为我们这里用到了mysql,qt不会把libmysql.dll集成到warehouse目标文件夹里面，所以报错了：driver not loaded
需要我们手动添加，直接将C:\Program Files\MySQL\MySQL Server 5.5\lib\ 下的libmysql.dll放在warehouse文件夹下面就好。


