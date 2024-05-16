adb（android debug bridge）常用指令有：

adb -v——列出所有指令说明

adb devices——列出所有连接的设备

adb kill-server——杀死adb调试桥

adb start-server——启动adb调试桥

adb install xxxx.apk——安装一个应用程序

adb unitall <包名>——卸载一个应用程序

adb -s 设备名称——指定某个设备

adb shell——远程连接手机命令行终端

adb pull <remote> <local>——从终端导出数据到电脑

adb push <local> <remote>——从电脑导入数据到终端