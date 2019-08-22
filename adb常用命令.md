- 启动服务: `adb start-server`
- 关闭服务: `adb kill-server`
- 获取设备号: `adb devices`
- 获取系统版本: `adb shell getprop ro.build.version.release`

- 发送文件到手机: `adb push 电脑端文件存储路径 手机端要存储路径`
- 拉取文件从手机: `adb pull 手机端存储文件路径 电脑端需要存储路径`

- 查看手机运行日志: `adb logcat | grep 包名`

- 手机shell 命令行: `adb shell`

- 获取app包名和启动名(手机必须打开对应app): `adb shell dumpsys window windows | grep mFocusedApp`

- 安装apk到手机: `adb install ,apk文件存储路径`
- 卸载app从手机: `adb uninstall 包名`

- 获取app启动时间: `adb shell am start -W 包名/启动名`
- TotalTime:app 自身启动时间
- WaitTime:系统启动应用时间
