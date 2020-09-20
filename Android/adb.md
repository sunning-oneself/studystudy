# adb

1. 显示当前运行的全部设备：

adb devices

2. 截图

adb shell screencap -p /sdcard/1.png

3. 录制视频

adb shell screenrecord /sdcard/1.mp4

4. 安装

adb install [-r] xxx.apk  // -r:强制安装

adb shell pm install [-r] /data/local/tmp/xxx.apk   //安装的apk源自于设备中

5. 查看包名

adb shell pm list packages  // 打印设备/模拟器上的所有软件包

adb shell pm list packages -3  // 只输出第三方的包

6. ps命令查找进程

adb shell ps | grep monkey

7. kill命令结束进程

adb shell kill 进程号

