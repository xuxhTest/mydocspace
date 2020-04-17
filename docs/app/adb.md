# ADB Debugging #
## adb devices ##
获取设备列表及设备详细信息(-l)

    adb devices
	adb devices -l
![](..\images\app\adb1.png)
## adb get-state ##
获取设备状态

![](..\images\app\adb2.png)

设备的状态有 3 钟，device , offline , unknown
device：设备正常连接

offline：连接出现异常，设备无响应

unknown：没有连接设备

## adb forward ##

list all forward socket connections

    adb forward --list
set up port forwarding

    adb forward tcp:6123 tcp:7123
## adb kill-server ##
terminates the adb server process

    adb kill-server
> Notes: kill the server if it is running. (terminal adb.exe process)
# Wireless #
## adb connect ##
STEP 1.

Set the target device to listen for a TCP/IP connection on port 5555

disconnect the USB cable from the Android device
    adb tcpip 5555
STEP 2.

Connect to a device over Wi-Fi.

find your Android device IP address at Settings > About phone > Status > IP address
    adb connect 192.168.100.12
STEP 3.

Confirm that your host computer is connected to the Android device over Wi-Fi

    adb devices
List of devices attached
192.168.100.12:5555 device
## adb usb ##
Restarting in USB mode

    adb usb
# Package Manager #
## adb install ##
app installation - push a single package to the device and install it

    adb install test.apk
app installation - push multiple APKs to the device for a single package and install them

    adb install-multiple test.apk test2.apk
app installation - push one or more packages to the device and install them atomically

    adb install-multi-package test.apk demo.apk
replace existing application

reinstall an existing app, keeping its data
    adb install -r test.apk
allow test packages

    adb install -t test.apk
allow version code downgrade

debuggable packages only
    adb install -d test.apk
grant all runtime permissions

Grant all permissions listed in the app manifest
    adb install -g test.apk
cause the app to be installed as an ephemeral install app

    adb install --instant test.apk
use fast deploy

    adb install --fastdeploy test.apk
always push APK to device and invoke Package Manager as separate steps

    adb install --no-streaming test.apk
## adb uninstall ##
remove this app package from the device

    adb uninstall test.apk
Keep the data and cache directories around after package removal

    adb uninstall -k test.apk
## adb shell pm list packages ##
Prints all packages

    adb shell pm list packages
see their associated APK file

    adb shell pm list packages -f
all known packages

but excluding APEXes (Android Pony EXpress)
    adb shell pm list packages -a
only show APEX packages

    adb shell pm list packages --apex-only
filter to only show disabled packages

    adb shell pm list packages -d
filter to only show enabled packages

    adb shell pm list packages -e
filter to only show system packages

    adb shell pm list packages -s
filter to only show third party packages

    adb shell pm list packages -3
see the installer for the packages

    adb shell pm list packages -i
ignored (used for compatibility with older releases)

    adb shell pm list packages -l
also show the package UID

    adb shell pm list packages -U
also include uninstalled packages

    adb shell pm list packages -u
also show the version code

    adb shell pm list packages --show-versioncode
filter to only show packages with the given UID

    adb shell pm list packages --uid UID
only list packages belonging to the given user

    adb shell pm list packages --user USER_ID
## adb shell pm path ##
Print the path to the .apk of the given installed package name

    adb shell pm path com.android.chrome
## adb shell pm clear ##
Deletes all data associated with a package.

adb shell pm clear <PACKAGE>
    adb shell pm clear com.test.abc
> Notes: clearing app data, cache
# File Manager #
## adb pull ##
copy files/dirs from device

To copy a file or directory and its sub-directories from the Android device
    adb  pull /mnt/sdcard/Download/test.apk pc.apk
preserve file timestamp and mode.

    adb  pull -a /mnt/sdcard/Download/test.apk pc.apk
## adb push ##
copy local files/directories to Android device

    adb push pc.apk /mnt/sdcard/Download/test.apk
only push files that are newer on the host than the Android device

    adb push --sync pc.apk /mnt/sdcard/Download/test.apk
## adb shell ls cd rm mkdir touch pwd cp mv ##
# Network #
## adb shell netstat ##
Display networking information.

Default is netstat -tuwx
    adb shell netstat
Routing table

    adb shell netstat -r
All sockets (not just connected)

    adb shell netstat -a
Listening server sockets

    adb shell netstat -l
TCP sockets

    adb shell netstat -t
UDP sockets

    adb shell netstat -u
Raw sockets

    adb shell netstat -w
Unix sockets

    adb shell netstat -x
Extended info

    adb shell netstat -e
Don't resolve names

    adb shell netstat -n
Wide display

    adb shell netstat -w
Show PID/program name of sockets

    adb shell netstat -p
## adb shell ping ##
ping (Packet Internet Groper) is a network administration utility used to testing, and diagnosing network connectivity issues

    adb shell ping
> Notes: press Ctrl-C to stop ping
Specifies the number of echo Request messages sent

    adb shell ping -c 4
Specifies the amount of time, in milliseconds, to wait for the echo Reply message that corresponds to a given echo Request message to be received

> The default time-out is 4000 (4 seconds)
    adb shell ping -W 200 127.0.0.1
Interval in seconds

> By default, interval is 1 second
    adb shell ping -i 2 127.0.0.1
## adb shell netcfg ##
Network configuration.

    adb shell netcfg
> Notes: /system/bin/sh: netcfg: not found in Android M or higher.
Display or configure network interface.

    adb shell ifconfig
## adb shell ip ##
get wlan0 (Wi-Fi) IP address

    adb shell ip addr show wlan0
route table

    adb shell ip route
ARP table

    adb shell ip neighbour
# Logcat #
## adb logcat ##
Prints log data to the screen.

adb logcat [option] [filter-specs]
adb logcat
> Notes: press Ctrl-C to stop monitor
> 
    adb logcat *:V lowest priority, filter to only show Verbose level
    adb logcat *:D filter to only show Debug level
    adb logcat *:I filter to only show Info level
    adb logcat *:W filter to only show Warning level
    adb logcat *:E filter to only show Error level
    adb logcat *:F filter to only show Fatal level
    adb logcat *:S Silent, highest priority, on which nothing is ever printed
adb logcat -b <Buffer>

    adb logcat -b radio View the buffer that contains radio/telephony related messages.

    adb logcat -b event View the buffer containing events-related messages.
    adb logcat -b main default
    adb logcat -c Clears the entire log and exits.
    adb logcat -d Dumps the log to the screen and exits.
    adb logcat -f test.logs Writes log message output to test.logs .
    adb logcat -g Prints the size of the specified log buffer and exits.
    adb logcat -n <count> Sets the maximum number of rotated logs to <count>. 
> Notes: The default value is 4. Requires the -r option.
> 
    adb logcat -r <kbytes> Rotates the log file every <kbytes> of output.

> Notes: The default value is 16. Requires the -f option.
> 
    adb logcat -s Sets the default filter spec to silent.
    adb logcat -v <format>
    adb logcat -v brief Display priority/tag and PID of the process issuing the message (default format).
    adb logcat -v process Display PID only.)
    adb logcat -v tag Display the priority/tag only.
    adb logcat -v raw Display the raw log message, with no other metadata fields.
    adb logcat -v time Display the date, invocation time, priority/tag, and PID of the process issuing the message.
    adb logcat -v threadtime Display the date, invocation time, priority, tag, and the PID and TID of the thread issuing the message.
    adb logcat -v long Display all metadata fields and separate messages with blank lines.


## adb shell dumpsys ##
To dump all services

    adb shell dumpsys
only list services, do not dump them


    adb shell dumpsys -l
Get Android device battery info

    adb shell dumpsys battery
## adb shell dumpstate ##
dump Android device state.

    adb shell dumpstate
> dumpstate not working with Android 10.
dump the Android device dumpstate, dumpsys and logcat outs.

    adb bugreport
# Screenshot #
## adb shell screencap ##
The screencap command is a shell utility for taking a screenshot of a device display

    adb shell screencap /mnt/sdcard/Download/test.png
> Notes: If FILENAME is not given, the results will be printed to stdout.
To copy screenshot from Android Device.

    adb pull /mnt/sdcard/Download/test.png test.png
## adb shell screenrecord ##
Android screenrecord v1.2. Records the device's display to a .mp4 file

    adb shell screenrecord /mnt/sdcard/Download/test.mp4

> Recording continues until Ctrl-C is hit or the time limit is reached

Set the video size, e.g. "1280x720". Default is the device's main display resolution (if supported), 1280x720 if not. For best results, use a size supported by the AVC encoder.

    adb shell screenrecord --size 1280x720 /mnt/sdcard/Download/test.mp4
Set the video bit rate, in bits per second. Value may be specified as bits or megabits, e.g. '4000000' is equivalent to '4M'. Default 20Mbps.

    adb shell screenrecord --bit-rate 4000000 /mnt/sdcard/Download/test.mp4
Rotates the output 90 degrees. This feature is experimental.

    adb shell screenrecord --rotate /mnt/sdcard/Download/test.mp4
Add additional information, such as a timestamp overlay, that is helpful in videos captured to illustrate bugs.

    adb shell screenrecord --bugreport /mnt/sdcard/Download/test.mp4
Set the maximum recording time, in seconds. Default / maximum is 180
    
    adb shell screenrecord --time-limit=120 /mnt/sdcard/Download/test.mp4
Display interesting information on stdout

    adb shell screenrecord --verbose /mnt/sdcard/Download/test.mp4
> Audio is not recorded with the video file. Rotation of the screen during recording is not supported. If the screen does rotate during recording, some of the screen is cut off in the recording.

# System #
# adb root #
restart adbd with root permissions

    adb root
restart adbd without root permissions

    adb unroot
## adb sideload ##
sideload the given full OTA package

    adb sideload /mnt/sdcard/Download/ota.zip
> No Root Required
## adb shell ps ##
List processes. Which processes to show (selections may be comma separated lists)

    adb shell ps
All processes

    adb shell ps -A
filter PIDs (--pid)

    adb shell ps -p 1256
Show threads

    adb shell ps -t
## adb shell top ##
Show process activity in real time

    adb shell top
Cursor LEFT/RIGHT to change sort, UP/DOWN move list, space to force update, R to reverse sort, Q to exit
Show threads

    adb shell top -H
Show FIELDS (def PID,USER,PR,NI,VIRT,RES,SHR,S,%CPU,%MEM,TIME+,CMDLINE)

    adb shell top -o %CPU,%MEM,TIME+
Maximum number of tasks to show

    adb shell top -m 50
## adb shell getprop ##
Gets an Android system property, or lists them all

    adb shell getprop
Show property types instead of values

    adb shell getprop -T
Get SIM Operator

    adb shell getprop gsm.sim.operator.alpha
Get Device IEMI

    adb shell getprop ro.ril.oem.imei
## adb shell setprop ##
set property service

setprop <key> <value>
STEP 1.

    adb shell 
STEP 2.

    setprop service.adb.tcp.port 5555
