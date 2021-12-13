## This demo uses STM's NUCLEO F767ZI board running the TOPPERS OS to communicate with Azure IoT Central via MQTT.

# This demo requires the following projects
TOPPERS Project:
https://dev.toppers.jp/trac_user/contrib/browser/azure_iot_hub_f767zi/trunk
IDE environment:

https://code.visualstudio.com
Download the compilation environment

MSYS2:
https://www.msys2.org
$ pacman ?Syu
$ pacman ?Syu
$ pacman -S make

ARM Compiler:
https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads
gcc-arm-none-eabi-10-2020-q4-major-win32.exe

Select the [Extensions] icon [Ctl+Shift+X] in VSCODE
-C/C++ for Visual Studio Code
-Coretex-Debug
Installation
When you are ready, follow the steps below to create the environment
1. copy IDE/TOPPERS/wolfmqtt to trunk-473/trunk
2.VSCODE menu
[File]->[Add Folder to WorkSpace...].
Set up trunk-473/trunk/wolfmqtt

Modify the make file
app_iothub_client/Debug/Mkaefile

Add the include path
INCLUDES += -I$(SRCDIR)/... /wolfmqtt

Add library
$(SRCDIR)/... /wolfmqtt/Debug/libwolfmqtt.a 

Change the stack size
asp_baseplatform/monitor/monitor.h
#define MONITOR_STACK_SIZE 2046
2046 to 4096

app_iothub_client/src/command.c
Add
extern int Wolf_MQTT_main(int argc, char **argv);

app_iothub_client/src/command.c
	{"IOT", iothub_client_main},
Change iothub_client_main to Wolf_MQTT_main

Build
VSCODE Menu
[Terminal]->[Run Task]->[buld all]

Writing to the board
[Terminal]->[Run Task]->[write app]

Terminal settings
https://ja.osdn.net/projects/ttssh2/
Install Tera Term
Serial setting of COM3(If it is not in COM3, please check it in system)
Setup speed 115200


Wait for a while to get the time from NTP
Sun Dec 12 14:52:18 2021

Input the following
mon>device iot

Communication will be started.
