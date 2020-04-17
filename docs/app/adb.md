# ADB Debugging #
## adb devices ##
获取设备列表及设备详细信息(-l)

    adb devices
	adb devices -l
![](images\app\adb1.png)
## adb get-state ##
获取设备状态

![](images\app\adb2.png)

设备的状态有 3 钟，device , offline , unknown
device：设备正常连接

offline：连接出现异常，设备无响应

unknown：没有连接设备

## adb forward ##
## adb kill-server ##
# Wireless #
## adb connect ##
## adb usb ##
# Package Manager #
## adb install ##
## adb uninstall ##
## adb shell pm list packages ##
## adb shell pm path ##
## adb shell pm clear ##
# File Manager #
## adb pull ##
## adb push ##
## adb shell ls cd rm mkdir touch pwd cp mv ##
# Network #
## adb shell netstat ##
## adb shell ping ##
## adb shell netcfg ##
## adb shell ip ##
# Logcat #
## adb logcat ##
## adb shell dumpsys ##
## adb shell dumpstate ##
# Screenshot #
## adb shell screencap ##
## adb shell screenrecord ##
# System #
# adb root #
## adb sideload ##
## adb shell ps ##
## adb shell top ##
## adb shell getprop ##
## adb shell setprop ##