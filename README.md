# Win11_DynamicLighting

![](https://github.com/ableshih/Win11_DynamicLighting/blob/main/jpg/unnamed.jpg)

[![IMAGE ALT TEXT]()]([https://www.youtube.com/watch?v=1AXZpPtm2w0](https://www.youtube.com/watch?v=1AXZpPtm2w0) "Win11_DynamicLighting")

[![IMAGE ALT TEXT](https://github.com/ableshih/Win11_DynamicLighting/blob/main/jpg/unnamed.jpg)](https://www.youtube.com/watch?v=1AXZpPtm2w0 "Unity Snake Game")

# LampArray

## 步驟
1. WSL
2. Ubuntu
3. 第一次開啟 Ubuntu 可能會出現的錯誤
4. 安裝 Pico 環境
5. 確認路徑 CMakeCache.txt 內容
6. 都對了便可完成 cmake 會花一點時間
7. make blink
8. 成功後產生 \wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\blink\blink.uf2
9. 安裝 RP2040MacropadHidSample
10. fork of TinyUSB hid.h hid_device.h
11. git clone RP2040MacropadHidSample
12. sudo apt install build-essential
13. git submodule update --init
14. to src and setup CMake build directory
15. -DPICO_SDK_PATH=../../../../../../pico/pico-sdk
16. 改 PICO_SDK_PATH
17. make
    



### Product Name (Macropad)
```
\\wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\RP2040MacropadHidSample\src\usb_descriptors.c


\\wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\RP2040MacropadHidSample\src\build\macropad.uf2

D:\Code\Pico\RP2040MacropadHidSample\src\usb_descriptors.c
char const* string_desc_arr [] = {
    (const char[]) { 0x09, 0x04 }, // 0: is supported language is English (0x0409)
    "Adafruit",                    // 1: Manufacturer
    "Macropad_3",                    // 2: Product
    "RP2040 Pico",                 // 3: Serials, Should use chip ID
    "Macropad Serial",             // 4: CDC Interface
};


#define USB_VID   0xCafe
#define USB_PID           (0x4000 | _PID_MAP(CDC, 0) | _PID_MAP(MSC, 1) | _PID_MAP(HID, 2) | \
                           _PID_MAP(MIDI, 3) | _PID_MAP(VENDOR, 4) )


D:\Code\Pico\RP2040MacropadHidSample\src\Lighting\LampArray.c
    LampArrayAttributesReport report = {
        LAMPARRAY_LAMP_COUNT,
        LAMPARRAY_WIDTH,
        LAMPARRAY_HEIGHT,
        LAMPARRAY_DEPTH,
        LAMPARRAY_KIND,
        LAMPARRAY_UPDATE_INTERVAL
    };
    
D:\Code\Pico\RP2040MacropadHidSample\src\util.h
// Neopixel                         
#define NEOPIXEL                    19
#define NEOPIXEL_PIO                pio0
#define NEOPIXEL_BITRATE            800000
#define NEOPIXEL_COUNT              12

// LampArray Attributes
#define LAMPARRAY_LAMP_COUNT        NEOPIXEL_COUNT
#define LAMPARRAY_WIDTH             59000    // 5.9 cm 
#define LAMPARRAY_HEIGHT            104000   // 10.4 cm
#define LAMPARRAY_DEPTH             25000    // 2.5 cm (including rotary encoder)
#define LAMPARRAY_KIND              1        // LampArrayKindKeyboard

D:\Code\Pico\RP2040MacropadHidSample\src\hid_device.h
  HID_USAGE_PAGE ( HID_USAGE_PAGE_DESKTOP     )                    ,\


D:\Code\Pico\RP2040MacropadHidSample\src\hid.h
  HID_USAGE_PAGE_LIGHTING_AND_ILLUMINATION = 0x59,



D:\Code\Pico\RP2040MacropadHidSample\src\hid_device.h
#define TUD_HID_REPORT_DESC_LIGHTING(report_id) \
  HID_USAGE_PAGE ( HID_USAGE_PAGE_LIGHTING_AND_ILLUMINATION ),\
  HID_USAGE      ( HID_USAGE_LIGHTING_LAMP_ARRAY            ),\




macropad_1.uf2
macropad_2.uf2
macropad_3.uf2
macropad_4.uf2
```
---

```
改成
\wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\RP2040MacropadHidSample\src\build\CMakeCache.txt
export PICO_SDK_PATH=../../../../../../pico/pico-sdk


\\wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\RP2040MacropadHidSample\src\build\CMakeCache.txt

//Path to the Raspberry Pi Pico SDK
//PICO_SDK_PATH:PATH=../../../pico/pico-sdk
PICO_SDK_PATH=PATH=../../../../../../pico/pico-sdk


到 
https://github.com/rsolorzanomsft/tinyusb/tree/hid-lighting/src/class/hid

下載 hid.h hid_device.h

copy 到
\\wsl.localhost\Ubuntu\home\ab\pico\pico-sdk\lib\tinyusb\src\class\hid
```


---

`Pico` `Dynamic Lighting` `動態光效`

### 定義值單位 µm 微米
1mm毫米 = 1000.000µm 微米
#define LAMPARRAY_WIDTH             59000    // 5.9 cm 
#define LAMPARRAY_HEIGHT            104000   // 10.4 cm
#define LAMPARRAY_DEPTH             25000    // 2.5 cm (including rotary encoder)

### Pin Out
NEOPIXEL GPIO19 
LED GPIO13
SPEAKER_SHUTDOWN GPIO14
SPEAKER GPIO16 
OLED_CS GPIO22
OLED_RESET GPIO23
OLED_DC GPIO24
SCK GPIO26 
MOSI GPIO27 
MISO GPIO28 
SCL GPIO21 
SDA GPIO20 
BUTTON GPIO0
ROTB GPIO18
ROTA GPIO17
KEY1 GPIO1
...
KEY12 GPIO12
https://github.com/adafruit/Adafruit-MacroPad-RP2040-PCB/blob/main/Adafruit%20MacroPad%20RP2040%20Pinout.pdf

### 程式和功能 -> 開啟或關閉 Windows 功能

勾選 
```
Windows 子系統 Linux 版 
虛擬機器平台
```




### 用 PowerShell 安裝 Ubuntu
```
Windows PowerShell
著作權（C） Microsoft Corporation。保留擁有權利。

安裝最新的 PowerShell 以取得新功能和改進功能！https://aka.ms/PSWindows

PS C:\Windows\system32> wsl --install
已安裝 Windows 子系統 Linux 版。
以下是可安裝之有效發佈的清單。
使用 'wsl --install -d <Distro>' 安裝。

NAME                                   FRIENDLY NAME
Ubuntu                                 Ubuntu
Debian                                 Debian GNU/Linux
kali-linux                             Kali Linux Rolling
Ubuntu-18.04                           Ubuntu 18.04 LTS
Ubuntu-20.04                           Ubuntu 20.04 LTS
Ubuntu-22.04                           Ubuntu 22.04 LTS
OracleLinux_7_9                        Oracle Linux 7.9
OracleLinux_8_7                        Oracle Linux 8.7
OracleLinux_9_1                        Oracle Linux 9.1
openSUSE-Leap-15.5                     openSUSE Leap 15.5
SUSE-Linux-Enterprise-Server-15-SP4    SUSE Linux Enterprise Server 15 SP4
SUSE-Linux-Enterprise-15-SP5           SUSE Linux Enterprise 15 SP5
openSUSE-Tumbleweed                    openSUSE Tumbleweed
```

`PS C:\Windows\system32> wsl --install -d Ubuntu`
```
正在安裝：Ubuntu
已完成安裝 Ubuntu。
正在啟動 Ubuntu...

PS C:\Windows\system32>
```

```
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: ab
New password:
Retype new password:
passwd: password updated successfully
Installation successful!
適用於 Linux 的 Windows 子系統現已在 Microsoft Store 中提供!
您可以執行 'wsl.exe --update' 進行升級或瀏覽 https://aka.ms/wslstorepage
從 Microsoft Store 安裝 WSL 將會為您提供最新的 WSL 更新，且更快速。
如需詳細資訊，請瀏覽 https://aka.ms/wslstoreinfo

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.10.102.1-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This message is shown once a day. To disable it please create the
/home/ab/.hushlogin file.
ab@DESKTOP-BLKOVOI:~$
```



### 安裝 Windows 子系統 Linux 版
`PS C:\Windows\system32> wsl --update`
正在安裝：Windows 子系統 Linux 版
已完成安裝 Windows 子系統 Linux 版。

### Microsoft Store 可見同步安裝

程式集名稱

Ubuntu
Windows 子系統 Linux 版

在 檔案總管 會多出 Linux
因有安裝 Ubuntu 會出現 Ubuntu 目錄

### Linux 刪除所有 檔案及目錄 指令
`$ rm -r pico/`


--------------------------------------------------------
### 第一次開啟 WSL 子系統 可能會出現的錯誤
```
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ab@C940-PC:~$
```


#### 第一次開啟 Ubuntu 可能會出現的錯誤
```
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.90.1-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


This message is shown once a day. To disable it please create the
/home/ab/.hushlogin file.
ab@C940-PC:~$
```
### 修復指令
```
sudo apt-get update

touch ~/.sudo_as_admin_successful
```
--------------------------------------------------------

=================================
### 安裝 Pico 環境
https://www.electromaker.io/blog/article/getting-started-with-the-raspberry-pi-pico-w-cc-sdk

```
sudo apt install git
mkdir pico
cd pico
git clone https://github.com/raspberrypi/pico-sdk.git
git clone https://github.com/raspberrypi/pico-examples.git
cd pico-sdk
git submodule update --init
sudo apt update
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential 
cd ..
cd pico-examples
mkdir build
cd build
```

```
ab@DESKTOP-BLKOVOI:~$ sudo apt install git
[sudo] password for ab:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Suggested packages:
  git-daemon-run | git-daemon-sysvinit git-doc git-email git-gui gitk gitweb git-cvs git-mediawiki git-svn
The following packages will be upgraded:
  git
1 upgraded, 0 newly installed, 0 to remove and 101 not upgraded.
Need to get 3166 kB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 git amd64 1:2.34.1-1ubuntu1.10 [3166 kB]
Fetched 3166 kB in 4s (750 kB/s)
(Reading database ... 24137 files and directories currently installed.)
Preparing to unpack .../git_1%3a2.34.1-1ubuntu1.10_amd64.deb ...
Unpacking git (1:2.34.1-1ubuntu1.10) over (1:2.34.1-1ubuntu1.9) ...
Setting up git (1:2.34.1-1ubuntu1.10) ...
ab@DESKTOP-BLKOVOI:~$ mkdir pico
ab@DESKTOP-BLKOVOI:~$ cd pico
ab@DESKTOP-BLKOVOI:~/pico$ git clone https://github.com/raspberrypi/pico-sdk.git
Cloning into 'pico-sdk'...
remote: Enumerating objects: 7606, done.
remote: Counting objects: 100% (2261/2261), done.
remote: Compressing objects: 100% (426/426), done.
remote: Total 7606 (delta 1896), reused 1903 (delta 1816), pack-reused 5345
Receiving objects: 100% (7606/7606), 2.62 MiB | 4.89 MiB/s, done.
Resolving deltas: 100% (4170/4170), done.
ab@DESKTOP-BLKOVOI:~/pico$ git clone https://github.com/raspberrypi/pico-examples.git
Cloning into 'pico-examples'...
remote: Enumerating objects: 2810, done.
remote: Counting objects: 100% (195/195), done.
remote: Compressing objects: 100% (145/145), done.
remote: Total 2810 (delta 75), reused 143 (delta 47), pack-reused 2615
Receiving objects: 100% (2810/2810), 7.95 MiB | 3.18 MiB/s, done.
Resolving deltas: 100% (1408/1408), done.
ab@DESKTOP-BLKOVOI:~/pico$ cd pico-sdk
ab@DESKTOP-BLKOVOI:~/pico/pico-sdk$ git submodule update --init
Submodule 'lib/btstack' (https://github.com/bluekitchen/btstack.git) registered for path 'lib/btstack'
Submodule 'lib/cyw43-driver' (https://github.com/georgerobotics/cyw43-driver.git) registered for path 'lib/cyw43-driver'
Submodule 'lib/lwip' (https://github.com/lwip-tcpip/lwip.git) registered for path 'lib/lwip'
Submodule 'lib/mbedtls' (https://github.com/Mbed-TLS/mbedtls.git) registered for path 'lib/mbedtls'
Submodule 'tinyusb' (https://github.com/hathach/tinyusb.git) registered for path 'lib/tinyusb'
Cloning into '/home/ab/pico/pico-sdk/lib/btstack'...
Cloning into '/home/ab/pico/pico-sdk/lib/cyw43-driver'...
Cloning into '/home/ab/pico/pico-sdk/lib/lwip'...
Cloning into '/home/ab/pico/pico-sdk/lib/mbedtls'...
Cloning into '/home/ab/pico/pico-sdk/lib/tinyusb'...
Submodule path 'lib/btstack': checked out '72ef1732c954d938091467961e41f4aa9b976b34'
Submodule path 'lib/cyw43-driver': checked out '8ef38a6d32c54f850bff8f189bdca19ded33792a'
Submodule path 'lib/lwip': checked out '239918ccc173cb2c2a62f41a40fd893f57faf1d6'
Submodule path 'lib/mbedtls': checked out 'a77287f8fa6b76f74984121fdafc8563147435c8'
Submodule path 'lib/tinyusb': checked out '86c416d4c0fb38432460b3e11b08b9de76941bf5'
ab@DESKTOP-BLKOVOI:~/pico/pico-sdk$ sudo apt update
Hit:1 http://security.ubuntu.com/ubuntu jammy-security InRelease
Hit:2 http://archive.ubuntu.com/ubuntu jammy InRelease
Hit:3 http://archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:4 http://archive.ubuntu.com/ubuntu jammy-backports InRelease
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
101 packages can be upgraded. Run 'apt list --upgradable' to see them.
ab@DESKTOP-BLKOVOI:~/pico/pico-sdk$ sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  binutils-arm-none-eabi bzip2 cmake-data cpp cpp-11 dh-elpa-helper dpkg-dev emacsen-common fakeroot fontconfig-config
  fonts-dejavu-core g++ g++-11 gcc gcc-11 gcc-11-base gcc-12-base libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libarchive13 libasan6 libatomic1 libc-dev-bin libc-devtools libc6 libc6-dev libcc1-0
  libcrypt-dev libdeflate0 libdpkg-perl libfakeroot libfile-fcntllock-perl libfontconfig1 libfreetype6 libgcc-11-dev
  libgcc-s1 libgd3 libgomp1 libisl23 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libjsoncpp25 liblsan0 libmpc3
  libnewlib-dev libnsl-dev libquadmath0 librhash0 libstdc++-11-dev libstdc++-arm-none-eabi-dev
  libstdc++-arm-none-eabi-newlib libstdc++6 libtiff5 libtirpc-dev libtsan0 libubsan1 libwebp7 libxpm4 linux-libc-dev
  lto-disabled-list make manpages-dev rpcsvc-proto
Suggested packages:
  bzip2-doc cmake-doc ninja-build cmake-format cpp-doc gcc-11-locales debian-keyring g++-multilib g++-11-multilib
  gcc-11-doc gcc-multilib autoconf automake libtool flex bison gdb gcc-doc gcc-11-multilib lrzip glibc-doc bzr
  libgd-tools libnewlib-doc libstdc++-11-doc make-doc
Recommended packages:
  libnss-nis libnss-nisplus
The following NEW packages will be installed:
  binutils-arm-none-eabi build-essential bzip2 cmake cmake-data cpp cpp-11 dh-elpa-helper dpkg-dev emacsen-common
  fakeroot fontconfig-config fonts-dejavu-core g++ g++-11 gcc gcc-11 gcc-11-base gcc-arm-none-eabi
  libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libarchive13 libasan6 libatomic1
  libc-dev-bin libc-devtools libc6-dev libcc1-0 libcrypt-dev libdeflate0 libdpkg-perl libfakeroot
  libfile-fcntllock-perl libfontconfig1 libfreetype6 libgcc-11-dev libgd3 libgomp1 libisl23 libitm1 libjbig0
  libjpeg-turbo8 libjpeg8 libjsoncpp25 liblsan0 libmpc3 libnewlib-arm-none-eabi libnewlib-dev libnsl-dev libquadmath0
  librhash0 libstdc++-11-dev libstdc++-arm-none-eabi-dev libstdc++-arm-none-eabi-newlib libtiff5 libtirpc-dev libtsan0
  libubsan1 libwebp7 libxpm4 linux-libc-dev lto-disabled-list make manpages-dev rpcsvc-proto
The following packages will be upgraded:
  gcc-12-base libc6 libgcc-s1 libstdc++6
4 upgraded, 66 newly installed, 0 to remove and 97 not upgraded.
Need to get 518 MB of archives.
After this operation, 2817 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libc6 amd64 2.35-0ubuntu3.4 [3234 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 gcc-12-base amd64 12.3.0-1ubuntu1~22.04 [20.1 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libstdc++6 amd64 12.3.0-1ubuntu1~22.04 [699 kB]
Get:4 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libgcc-s1 amd64 12.3.0-1ubuntu1~22.04 [53.9 kB]
Get:5 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libc-dev-bin amd64 2.35-0ubuntu3.4 [20.3 kB]
Get:6 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-libc-dev amd64 5.15.0-86.96 [1338 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy/main amd64 libcrypt-dev amd64 1:4.4.27-1 [112 kB]
Get:8 http://archive.ubuntu.com/ubuntu jammy/main amd64 rpcsvc-proto amd64 1.4.2-0ubuntu6 [68.5 kB]
Get:9 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libtirpc-dev amd64 1.3.2-2ubuntu0.1 [192 kB]
Get:10 http://archive.ubuntu.com/ubuntu jammy/main amd64 libnsl-dev amd64 1.3.0-2build2 [71.3 kB]
Get:11 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libc6-dev amd64 2.35-0ubuntu3.4 [2100 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 gcc-11-base amd64 11.4.0-1ubuntu1~22.04 [20.2 kB]
Get:13 http://archive.ubuntu.com/ubuntu jammy/main amd64 libisl23 amd64 0.24-2build1 [727 kB]
Get:14 http://archive.ubuntu.com/ubuntu jammy/main amd64 libmpc3 amd64 1.2.1-2build1 [46.9 kB]
Get:15 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 cpp-11 amd64 11.4.0-1ubuntu1~22.04 [10.0 MB]
Get:16 http://archive.ubuntu.com/ubuntu jammy/main amd64 cpp amd64 4:11.2.0-1ubuntu1 [27.7 kB]
Get:17 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libcc1-0 amd64 12.3.0-1ubuntu1~22.04 [48.3 kB]
Get:18 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libgomp1 amd64 12.3.0-1ubuntu1~22.04 [126 kB]
Get:19 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libitm1 amd64 12.3.0-1ubuntu1~22.04 [30.2 kB]
Get:20 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libatomic1 amd64 12.3.0-1ubuntu1~22.04 [10.4 kB]
Get:21 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libasan6 amd64 11.4.0-1ubuntu1~22.04 [2282 kB]
Get:22 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 liblsan0 amd64 12.3.0-1ubuntu1~22.04 [1069 kB]
Get:23 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libtsan0 amd64 11.4.0-1ubuntu1~22.04 [2260 kB]
Get:24 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libubsan1 amd64 12.3.0-1ubuntu1~22.04 [976 kB]
Get:25 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libquadmath0 amd64 12.3.0-1ubuntu1~22.04 [154 kB]
Get:26 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libgcc-11-dev amd64 11.4.0-1ubuntu1~22.04 [2517 kB]
Get:27 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 gcc-11 amd64 11.4.0-1ubuntu1~22.04 [20.1 MB]
Get:28 http://archive.ubuntu.com/ubuntu jammy/main amd64 gcc amd64 4:11.2.0-1ubuntu1 [5112 B]
Get:29 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libstdc++-11-dev amd64 11.4.0-1ubuntu1~22.04 [2101 kB]
Get:30 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 g++-11 amd64 11.4.0-1ubuntu1~22.04 [11.4 MB]
Get:31 http://archive.ubuntu.com/ubuntu jammy/main amd64 g++ amd64 4:11.2.0-1ubuntu1 [1412 B]
Get:32 http://archive.ubuntu.com/ubuntu jammy/main amd64 make amd64 4.3-4.1build1 [180 kB]
Get:33 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libdpkg-perl all 1.21.1ubuntu2.2 [237 kB]
Get:34 http://archive.ubuntu.com/ubuntu jammy/main amd64 bzip2 amd64 1.0.8-5build1 [34.8 kB]
Get:35 http://archive.ubuntu.com/ubuntu jammy/main amd64 lto-disabled-list all 24 [12.5 kB]
Get:36 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 dpkg-dev all 1.21.1ubuntu2.2 [922 kB]
Get:37 http://archive.ubuntu.com/ubuntu jammy/main amd64 build-essential amd64 12.9ubuntu3 [4744 B]
Get:38 http://archive.ubuntu.com/ubuntu jammy/main amd64 libarchive13 amd64 3.6.0-1ubuntu1 [368 kB]
Get:39 http://archive.ubuntu.com/ubuntu jammy/main amd64 libjsoncpp25 amd64 1.9.5-3 [80.0 kB]
Get:40 http://archive.ubuntu.com/ubuntu jammy/main amd64 librhash0 amd64 1.4.2-1ubuntu1 [125 kB]
Get:41 http://archive.ubuntu.com/ubuntu jammy/main amd64 dh-elpa-helper all 2.0.9ubuntu1 [7610 B]
Get:42 http://archive.ubuntu.com/ubuntu jammy/main amd64 emacsen-common all 3.0.4 [14.9 kB]
Get:43 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 cmake-data all 3.22.1-1ubuntu1.22.04.1 [1913 kB]
Get:44 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 cmake amd64 3.22.1-1ubuntu1.22.04.1 [5013 kB]
Get:45 http://archive.ubuntu.com/ubuntu jammy/main amd64 libfakeroot amd64 1.28-1ubuntu1 [31.5 kB]
Get:46 http://archive.ubuntu.com/ubuntu jammy/main amd64 fakeroot amd64 1.28-1ubuntu1 [60.4 kB]
Get:47 http://archive.ubuntu.com/ubuntu jammy/main amd64 fonts-dejavu-core all 2.37-2build1 [1041 kB]
Get:48 http://archive.ubuntu.com/ubuntu jammy/main amd64 fontconfig-config all 2.13.1-4.2ubuntu5 [29.1 kB]
Setting up libtsan0:amd64 (11.4.0-1ubuntu1~22.04) ...
Setting up libjpeg8:amd64 (8c-2ubuntu10) ...
Setting up cpp-11 (11.4.0-1ubuntu1~22.04) ...
Setting up fontconfig-config (2.13.1-4.2ubuntu5) ...
Setting up gcc-arm-none-eabi (15:10.3-2021.07-4) ...
Setting up dpkg-dev (1.21.1ubuntu2.2) ...
Setting up libgcc-11-dev:amd64 (11.4.0-1ubuntu1~22.04) ...
Setting up gcc-11 (11.4.0-1ubuntu1~22.04) ...
Setting up cpp (4:11.2.0-1ubuntu1) ...
Setting up cmake (3.22.1-1ubuntu1.22.04.1) ...
Setting up libc6-dev:amd64 (2.35-0ubuntu3.4) ...
Setting up libtiff5:amd64 (4.3.0-6ubuntu0.5) ...
Setting up libfontconfig1:amd64 (2.13.1-4.2ubuntu5) ...
Setting up libstdc++-arm-none-eabi-dev (15:10.3-2021.07-4+17) ...
Setting up gcc (4:11.2.0-1ubuntu1) ...
Setting up libstdc++-arm-none-eabi-newlib (15:10.3-2021.07-4+17) ...
Setting up libgd3:amd64 (2.3.0-2ubuntu2) ...
Setting up libstdc++-11-dev:amd64 (11.4.0-1ubuntu1~22.04) ...
Setting up libc-devtools (2.35-0ubuntu3.4) ...
Setting up g++-11 (11.4.0-1ubuntu1~22.04) ...
Setting up g++ (4:11.2.0-1ubuntu1) ...
update-alternatives: using /usr/bin/g++ to provide /usr/bin/c++ (c++) in auto mode
Setting up build-essential (12.9ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
/sbin/ldconfig.real: /usr/lib/wsl/lib/libcuda.so.1 is not a symbolic link

ab@DESKTOP-BLKOVOI:~/pico/pico-sdk$ cd ..
ab@DESKTOP-BLKOVOI:~/pico$
```
----
```
ab@C940-PC:~$ rm -r pico/
ab@C940-PC:~$ sudo apt install git
[sudo] password for ab:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
git is already the newest version (1:2.34.1-1ubuntu1.10).
0 upgraded, 0 newly installed, 0 to remove and 47 not upgraded.
ab@C940-PC:~$ mkdir pico
ab@C940-PC:~$ cd pico
ab@C940-PC:~/pico$ git clone https://github.com/raspberrypi/pico-sdk.git
Cloning into 'pico-sdk'...
remote: Enumerating objects: 7606, done.
remote: Counting objects: 100% (1837/1837), done.
remote: Compressing objects: 100% (407/407), done.
remote: Total 7606 (delta 1523), reused 1496 (delta 1411), pack-reused 5769
Receiving objects: 100% (7606/7606), 2.90 MiB | 7.11 MiB/s, done.
Resolving deltas: 100% (4096/4096), done.
ab@C940-PC:~/pico$ git clone https://github.com/raspberrypi/pico-examples.git
Cloning into 'pico-examples'...
remote: Enumerating objects: 2810, done.
remote: Counting objects: 100% (195/195), done.
remote: Compressing objects: 100% (145/145), done.
remote: Total 2810 (delta 75), reused 143 (delta 47), pack-reused 2615
Receiving objects: 100% (2810/2810), 7.95 MiB | 8.79 MiB/s, done.
Resolving deltas: 100% (1408/1408), done.
ab@C940-PC:~/pico$ cd pico-sdk
ab@C940-PC:~/pico/pico-sdk$ git submodule update --init
Submodule 'lib/btstack' (https://github.com/bluekitchen/btstack.git) registered for path 'lib/btstack'
Submodule 'lib/cyw43-driver' (https://github.com/georgerobotics/cyw43-driver.git) registered for path 'lib/cyw43-driver'
Submodule 'lib/lwip' (https://github.com/lwip-tcpip/lwip.git) registered for path 'lib/lwip'
Submodule 'lib/mbedtls' (https://github.com/Mbed-TLS/mbedtls.git) registered for path 'lib/mbedtls'
Submodule 'tinyusb' (https://github.com/hathach/tinyusb.git) registered for path 'lib/tinyusb'
Cloning into '/home/ab/pico/pico-sdk/lib/btstack'...
Cloning into '/home/ab/pico/pico-sdk/lib/cyw43-driver'...
Cloning into '/home/ab/pico/pico-sdk/lib/lwip'...
Cloning into '/home/ab/pico/pico-sdk/lib/mbedtls'...
Cloning into '/home/ab/pico/pico-sdk/lib/tinyusb'...
Submodule path 'lib/btstack': checked out '72ef1732c954d938091467961e41f4aa9b976b34'
Submodule path 'lib/cyw43-driver': checked out '8ef38a6d32c54f850bff8f189bdca19ded33792a'
Submodule path 'lib/lwip': checked out '239918ccc173cb2c2a62f41a40fd893f57faf1d6'
Submodule path 'lib/mbedtls': checked out 'a77287f8fa6b76f74984121fdafc8563147435c8'
Submodule path 'lib/tinyusb': checked out '86c416d4c0fb38432460b3e11b08b9de76941bf5'
ab@C940-PC:~/pico/pico-sdk$ sudo apt update
Hit:1 http://archive.ubuntu.com/ubuntu jammy InRelease
Get:2 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]
Hit:4 http://archive.ubuntu.com/ubuntu jammy-backports InRelease
Fetched 229 kB in 2s (134 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
47 packages can be upgraded. Run 'apt list --upgradable' to see them.



ab@C940-PC:~/pico/pico-sdk$ sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
build-essential is already the newest version (12.9ubuntu3).
gcc-arm-none-eabi is already the newest version (15:10.3-2021.07-4).
libnewlib-arm-none-eabi is already the newest version (3.3.0-1.3).
cmake is already the newest version (3.22.1-1ubuntu1.22.04.1).
0 upgraded, 0 newly installed, 0 to remove and 47 not upgraded.



ab@C940-PC:~/pico/pico-sdk$ cd ..
ab@C940-PC:~/pico$ cd pico-examples
ab@C940-PC:~/pico/pico-examples$ mkdir build
ab@C940-PC:~/pico/pico-examples$ cd build
ab@C940-PC:~/pico/pico-examples/build$ export PICO_SDK_PATH=../../../pico/pico-sdk
ab@C940-PC:~/pico/pico-examples/build$ cd ../../../pico/pico-sdk
ab@C940-PC:~/pico/pico-sdk$ cd ..
ab@C940-PC:~/pico$ cd pico-examples/build/
ab@C940-PC:~/pico/pico-examples/build$ export PICO_SDK_PATH=../../../pico/pico-sdk


ab@C940-PC:~/pico/pico-examples/build$ cmake -DPICO_BOARD=pico_w ..
Using PICO_SDK_PATH from environment ('../../../pico/pico-sdk')
PICO_SDK_PATH is /home/ab/pico/pico-sdk
Defaulting PICO_PLATFORM to rp2040 since not specified.
Defaulting PICO platform compiler to pico_arm_gcc since not specified.
-- Defaulting build type to 'Release' since not specified.
PICO compiler is pico_arm_gcc
-- The C compiler identification is GNU 10.3.1
-- The CXX compiler identification is GNU 10.3.1
-- The ASM compiler identification is GNU
-- Found assembler: /usr/bin/arm-none-eabi-gcc
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/arm-none-eabi-gcc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/arm-none-eabi-g++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
Build type is Release
PICO target board is pico_w.
Using CMake board configuration from /home/ab/pico/pico-sdk/src/boards/pico_w.cmake
Using board configuration from /home/ab/pico/pico-sdk/src/boards/include/boards/pico_w.h
-- Found Python3: /usr/bin/python3.10 (found version "3.10.12") found components: Interpreter
TinyUSB available at /home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040; enabling build support for USB.
BTstack available at /home/ab/pico/pico-sdk/lib/btstack
cyw43-driver available at /home/ab/pico/pico-sdk/lib/cyw43-driver
Pico W Bluetooth build support available.
lwIP available at /home/ab/pico/pico-sdk/lib/lwip
Pico W Wi-Fi build support available.
mbedtls available at /home/ab/pico/pico-sdk/lib/mbedtls
Skipping some Pico W examples as WIFI_SSID is not defined
Skipping some Pico W BTstack examples that require pico-extras
Adding 19 BTstack examples of type 'background'
Skipping TinyUSB dual examples, as TinyUSB hw/mcu/raspberry_pi/Pico-PIO-USB submodule unavailable
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ab/pico/pico-examples/build




ab@C940-PC:~/pico/pico-examples/build$ cd blink
ab@C940-PC:~/pico/pico-examples/build/blink$ make
Creating directories for 'ELF2UF2Build'
No download step for 'ELF2UF2Build'
No update step for 'ELF2UF2Build'
No patch step for 'ELF2UF2Build'
Performing configure step for 'ELF2UF2Build'
-- The C compiler identification is GNU 11.4.0
-- The CXX compiler identification is GNU 11.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ab/pico/pico-examples/build/elf2uf2
Performing build step for 'ELF2UF2Build'
[ 50%] Building CXX object CMakeFiles/elf2uf2.dir/main.cpp.o
[100%] Linking CXX executable elf2uf2
[100%] Built target elf2uf2
No install step for 'ELF2UF2Build'
Completed 'ELF2UF2Build'
Built target ELF2UF2Build
Scanning dependencies of target bs2_default
Building ASM object pico-sdk/src/rp2_common/boot_stage2/CMakeFiles/bs2_default.dir/compile_time_choice.S.obj
Linking ASM executable bs2_default.elf
Built target bs2_default
Generating bs2_default.bin
Generating bs2_default_padded_checksummed.S
Built target bs2_default_padded_checksummed_asm
Scanning dependencies of target blink
Building C object blink/CMakeFiles/blink.dir/blink.c.obj
/home/ab/pico/pico-examples/blink/blink.c: In function 'main':
/home/ab/pico/pico-examples/blink/blink.c:11:2: warning: #warning blink example requires a board with a regular LED [-Wcpp]
   11 | #warning blink example requires a board with a regular LED
      |  ^~~~~~~
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdlib/stdlib.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_gpio/gpio.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_platform/platform.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_claim/claim.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_sync/sync.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_irq/irq.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_irq/irq_handler_chain.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_sync/sem.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_sync/lock_core.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_sync/mutex.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_sync/critical_section.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_time/time.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_time/timeout_helper.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_timer/timer.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_util/datetime.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_util/pheap.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_util/queue.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_uart/uart.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_clocks/clocks.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_pll/pll.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_vreg/vreg.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_watchdog/watchdog.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_xosc/xosc.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_divider/divider.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_runtime/runtime.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_printf/printf.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_bit_ops/bit_ops_aeabi.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_bootrom/bootrom.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_divider/divider.S.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_aeabi.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_init_rom.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_math.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_v1_rom_shim.S.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_int64_ops/pico_int64_ops_aeabi.S.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_aeabi.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_init_rom.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_math.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_v1_rom_shim.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_malloc/pico_malloc.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_mem_ops/mem_ops_aeabi.S.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/crt0.S.obj
Building CXX object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/new_delete.cpp.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/binary_info.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio/stdio.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_uart/stdio_uart.c.obj
Linking CXX executable blink.elf
Built target blink
ab@C940-PC:~/pico/pico-examples/build/blink$ make
Performing build step for 'ELF2UF2Build'
Consolidate compiler generated dependencies of target elf2uf2
[100%] Built target elf2uf2
No install step for 'ELF2UF2Build'
Completed 'ELF2UF2Build'
Built target ELF2UF2Build
Built target bs2_default
Built target bs2_default_padded_checksummed_asm
Consolidate compiler generated dependencies of target blink
Built target blink




ab@C940-PC:~/pico/pico-examples/build/blink$ cd ..
ab@C940-PC:~/pico/pico-examples/build$ git clone https://github.com/microsoft/RP2040MacropadHidSample.git
Cloning into 'RP2040MacropadHidSample'...
remote: Enumerating objects: 78, done.
remote: Counting objects: 100% (78/78), done.
remote: Compressing objects: 100% (59/59), done.
remote: Total 78 (delta 33), reused 49 (delta 17), pack-reused 0
Receiving objects: 100% (78/78), 5.61 MiB | 7.04 MiB/s, done.
Resolving deltas: 100% (33/33), done.
ab@C940-PC:~/pico/pico-examples/build$ sudo apt install build-essential
[sudo] password for ab:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
build-essential is already the newest version (12.9ubuntu3).
0 upgraded, 0 newly installed, 0 to remove and 47 not upgraded.




ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ export PICO_SDK_PATH=../../../../../../pico/pico-sdk

ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ cmake -DPICO_BOARD=adafruit_macropad_rp2040 ..
PICO_SDK_PATH is /home/ab/pico/pico-sdk
Defaulting PICO_PLATFORM to rp2040 since not specified.
Defaulting PICO platform compiler to pico_arm_gcc since not specified.
-- Defaulting build type to 'Release' since not specified.
PICO compiler is pico_arm_gcc
-- The C compiler identification is GNU 10.3.1
-- The CXX compiler identification is GNU 10.3.1
-- The ASM compiler identification is GNU
-- Found assembler: /usr/bin/arm-none-eabi-gcc
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/arm-none-eabi-gcc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/arm-none-eabi-g++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
Build type is Release
PICO target board is adafruit_macropad_rp2040.
Using board configuration from /home/ab/pico/pico-sdk/src/boards/include/boards/adafruit_macropad_rp2040.h
-- Found Python3: /usr/bin/python3.10 (found version "3.10.12") found components: Interpreter
TinyUSB available at /home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040; enabling build support for USB.
BTstack available at /home/ab/pico/pico-sdk/lib/btstack
cyw43-driver available at /home/ab/pico/pico-sdk/lib/cyw43-driver
Pico W Bluetooth build support available.
lwIP available at /home/ab/pico/pico-sdk/lib/lwip
mbedtls available at /home/ab/pico/pico-sdk/lib/mbedtls
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ab/pico/pico-examples/build/RP2040MacropadHidSample/src/build





ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ make
[  2%] Built target bs2_default
[  4%] Built target bs2_default_padded_checksummed_asm
[  5%] Performing build step for 'PioasmBuild'
[100%] Built target pioasm
[  6%] No install step for 'PioasmBuild'
[  7%] Completed 'PioasmBuild'
[ 12%] Built target PioasmBuild
[ 13%] Built target macropad_neopixel_pio_h
[ 14%] Performing build step for 'ELF2UF2Build'
[100%] Built target elf2uf2
[ 15%] No install step for 'ELF2UF2Build'
[ 15%] Completed 'ELF2UF2Build'
[ 20%] Built target ELF2UF2Build
Consolidate compiler generated dependencies of target macropad
[ 21%] Building C object CMakeFiles/macropad.dir/macropad.c.obj
[ 22%] Building C object CMakeFiles/macropad.dir/usb_descriptors.c.obj
[ 23%] Building C object CMakeFiles/macropad.dir/Keys/Keys.c.obj
[ 24%] Building C object CMakeFiles/macropad.dir/Encoder/Encoder.c.obj
[ 25%] Building C object CMakeFiles/macropad.dir/Lighting/Neopixel.c.obj
[ 26%] Building C object CMakeFiles/macropad.dir/Lighting/LampArray.c.obj
[ 27%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdlib/stdlib.c.obj
[ 28%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_gpio/gpio.c.obj
[ 29%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_platform/platform.c.obj
[ 30%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_claim/claim.c.obj
[ 31%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_sync/sync.c.obj
[ 32%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_irq/irq.c.obj
[ 33%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_irq/irq_handler_chain.S.obj
[ 34%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_sync/sem.c.obj
[ 35%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_sync/lock_core.c.obj
[ 36%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_sync/mutex.c.obj
[ 37%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_sync/critical_section.c.obj
[ 38%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_time/time.c.obj
[ 39%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_time/timeout_helper.c.obj
[ 40%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_timer/timer.c.obj
[ 41%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_util/datetime.c.obj
[ 42%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_util/pheap.c.obj
[ 43%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_util/queue.c.obj
[ 44%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_uart/uart.c.obj
[ 45%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_clocks/clocks.c.obj
[ 46%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_pll/pll.c.obj
[ 47%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_vreg/vreg.c.obj
[ 48%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_watchdog/watchdog.c.obj
[ 50%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_xosc/xosc.c.obj
[ 50%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_divider/divider.S.obj
[ 51%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_runtime/runtime.c.obj
[ 52%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_printf/printf.c.obj
[ 53%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_bit_ops/bit_ops_aeabi.S.obj
[ 54%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_bootrom/bootrom.c.obj
[ 55%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_divider/divider.S.obj
[ 56%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_aeabi.S.obj
[ 57%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_init_rom.c.obj
[ 58%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_math.c.obj
[ 59%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_v1_rom_shim.S.obj
[ 60%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_int64_ops/pico_int64_ops_aeabi.S.obj
[ 61%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_aeabi.S.obj
[ 62%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_init_rom.c.obj
[ 63%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_math.c.obj
[ 64%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_v1_rom_shim.S.obj
[ 65%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_malloc/pico_malloc.c.obj
[ 66%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_mem_ops/mem_ops_aeabi.S.obj
[ 67%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/crt0.S.obj
[ 68%] Building CXX object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/new_delete.cpp.obj
[ 69%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/binary_info.c.obj
[ 70%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio/stdio.c.obj
[ 71%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_uart/stdio_uart.c.obj
[ 72%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_usb/reset_interface.c.obj
[ 73%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_usb/stdio_usb.c.obj
[ 74%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_usb/stdio_usb_descriptors.c.obj
[ 75%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_unique_id/unique_id.c.obj
[ 76%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_flash/flash.c.obj
[ 77%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040/dcd_rp2040.c.obj
[ 78%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040/rp2040_usb.c.obj
[ 79%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/device/usbd.c.obj
[ 80%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/device/usbd_control.c.obj
[ 81%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/audio/audio_device.c.obj
[ 82%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/cdc/cdc_device.c.obj
[ 83%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/dfu/dfu_device.c.obj
[ 84%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/dfu/dfu_rt_device.c.obj
[ 85%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/hid/hid_device.c.obj
[ 86%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/midi/midi_device.c.obj
[ 87%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/msc/msc_device.c.obj
[ 88%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/net/ecm_rndis_device.c.obj
[ 89%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/net/ncm_device.c.obj
[ 90%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/usbtmc/usbtmc_device.c.obj
[ 91%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/vendor/vendor_device.c.obj
[ 92%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/video/video_device.c.obj
[ 93%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/tusb.c.obj
[ 94%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/common/tusb_fifo.c.obj
[ 95%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_fix/rp2040_usb_device_enumeration/rp2040_usb_device_enumeration.c.obj
[ 96%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_multicore/multicore.c.obj
[ 97%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_pio/pio.c.obj
[ 98%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/hw/bsp/rp2040/family.c.obj
[100%] Linking CXX executable macropad.elf
[100%] Built target macropad
ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ make


ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$
```
----
### 錯

#### Export e要小寫 否則出錯
`Export PICO_SDK_PATH=../../pico-sdk/`

#### 改成
`export PICO_SDK_PATH=../../../../../../pico/pico-sdk`
`export PICO_SDK_PATH=../../../pico/pico-sdk`

#### 確認路徑 CMakeCache.txt 內容
```
\\wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\CMakeCache.txt

//Path to the Raspberry Pi Pico SDK
PICO_SDK_PATH:PATH=../../../pico/pico-sdk
```

#### 都對了便可完成 cmake 會花一點時間
```
cmake -DPICO_BOARD=pico_w ..
```
---

```
ab@DESKTOP-BLKOVOI:~/pico$ cd pico-examples
ab@DESKTOP-BLKOVOI:~/pico/pico-examples$ mkdir build
ab@DESKTOP-BLKOVOI:~/pico/pico-examples$ cd build
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$ cd ../../../pico/pico-sdk
ab@DESKTOP-BLKOVOI:~/pico/pico-sdk$ cd ..
ab@DESKTOP-BLKOVOI:~/pico$ cd pico-examples/build/
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$ export 
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$
```


---

```
ab@DESKTOP-BLKOVOI:~/pico$ cd pico-examples
ab@DESKTOP-BLKOVOI:~/pico/pico-examples$ mkdir build
ab@DESKTOP-BLKOVOI:~/pico/pico-examples$ cd build

ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$ cd ../../../pico/pico-sdk
ab@DESKTOP-BLKOVOI:~/pico/pico-sdk$ cd ..
ab@DESKTOP-BLKOVOI:~/pico$ cd pico-examples/build/


ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$ export PICO_SDK_PATH=../../../pico/pico-sdk
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$ cmake -DPICO_BOARD=pico_w ..
PICO_SDK_PATH is /home/ab/pico/pico-sdk
Defaulting PICO_PLATFORM to rp2040 since not specified.
Defaulting PICO platform compiler to pico_arm_gcc since not specified.
-- Defaulting build type to 'Release' since not specified.
PICO compiler is pico_arm_gcc
-- The C compiler identification is GNU 10.3.1
-- The CXX compiler identification is GNU 10.3.1
-- The ASM compiler identification is GNU
-- Found assembler: /usr/bin/arm-none-eabi-gcc
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/arm-none-eabi-gcc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/arm-none-eabi-g++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
Build type is Release
PICO target board is pico_w.
Using CMake board configuration from /home/ab/pico/pico-sdk/src/boards/pico_w.cmake
Using board configuration from /home/ab/pico/pico-sdk/src/boards/include/boards/pico_w.h
-- Found Python3: /usr/bin/python3.10 (found version "3.10.6") found components: Interpreter
TinyUSB available at /home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040; enabling build support for USB.
BTstack available at /home/ab/pico/pico-sdk/lib/btstack
cyw43-driver available at /home/ab/pico/pico-sdk/lib/cyw43-driver
Pico W Bluetooth build support available.
lwIP available at /home/ab/pico/pico-sdk/lib/lwip
Pico W Wi-Fi build support available.
mbedtls available at /home/ab/pico/pico-sdk/lib/mbedtls
Skipping some Pico W examples as WIFI_SSID is not defined
Skipping some Pico W BTstack examples that require pico-extras
Adding 19 BTstack examples of type 'background'
Skipping TinyUSB dual examples, as TinyUSB hw/mcu/raspberry_pi/Pico-PIO-USB submodule unavailable
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ab/pico/pico-examples/build
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$
```


### make blink
cd blink
make

#### 成功後產生
\\wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\blink\blink.uf2



=================================
### 官方 安裝




https://github.com/microsoft/RP2040MacropadHidSample

請注意，該專案是使用最新的 Ubuntu WSL 建置和測試的。其他發行版和 Windows 版本的 Pico SDK 應該可以工作，但這些選項尚未得到驗證。
Macropad Setup instructions
Note, that this project was built and tested using the latest Ubuntu WSL. Other distributions and the Windows version of the Pico SDK should work, but those options have not been verified.

1. 將 WSL 安裝到 Windows 電腦上
   Install WSL onto Windows Machine
2. git clone該專案進入 WSL 發行版。該目錄現在將成為專案目錄。
   git clone this project into WSL distribtion. This directory will now be the project directory.
   
`git clone https://github.com/microsoft/RP2040MacropadHidSample.git`
   
3. 安裝建置依賴項。
   Install build dependencies.
`$ sudo apt install build-essential`

```
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$ git clone https://github.com/microsoft/RP2040MacropadHidSample.git
Cloning into 'RP2040MacropadHidSample'...
remote: Enumerating objects: 78, done.
remote: Counting objects: 100% (78/78), done.
remote: Compressing objects: 100% (59/59), done.
remote: Total 78 (delta 33), reused 49 (delta 17), pack-reused 0
Receiving objects: 100% (78/78), 5.61 MiB | 3.95 MiB/s, done.
Resolving deltas: 100% (33/33), done.
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$ sudo apt install build-essential
[sudo] password for ab:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
build-essential is already the newest version (12.9ubuntu3).
0 upgraded, 0 newly installed, 0 to remove and 97 not upgraded.
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build$
```

4. 請依照 https://github.com/raspberrypi/pico-sdk 中的 Pico SDK 設定說明進行步驟 2c。（對於步驟 2，該項目是透過克隆 SDK 來設定的）
   Follow Pico SDK setup instructions from https://github.com/raspberrypi/pico-sdk up through step 2c. (For step 2, this project was set up by cloning the SDK)
   
5. cd 到SDK目錄並運行git submodule update --init
   cd to the SDK directory and run git submodule update --init
6. 更新 TinyUSB hid 標頭以包含 LampArray。導航到[TinyUSB 的分支](https://github.com/rsolorzanomsft/tinyusb/tree/hid-lighting/src/class/hid)。將頭檔 hid.h 和 hid_device.h 複製到 Pico SDK 路徑中的 TinyUSB 庫，即<PicoSdkRoot>/lib/tinyusb/src/class/hid/。TODO： TinyUSB 中的PR進入後，刪除此步驟

   Update TinyUSB hid header to include LampArray. Navigate to [fork of TinyUSB](https://github.com/rsolorzanomsft/tinyusb/tree/hid-lighting/src/class/hid). Copy headers hid.h and hid_device.h to TinyUSB library in Pico SDK path, i.e. <PicoSdkRoot>/lib/tinyusb/src/class/hid/. TODO: Once PR in TinyUSB goes in, remove this step
    
    `https://github.com/rsolorzanomsft/tinyusb`
    
### 要直接下載     
```
src/class/hid/hid_device.h
    32.8 KB (33,674 位元組)
src/class/hid/hid.h 
    50.3 KB (51,536 位元組)
https://github.com/rsolorzanomsft/tinyusb/blob/hid-lighting/src/class/hid/hid.h
https://github.com/rsolorzanomsft/tinyusb/blob/hid-lighting/src/class/hid/hid_device.h 
```   
    
7. cd 到<ProjectDirectory>/src並設定 CMake 建置目錄：
   cd to <ProjectDirectory>/src and setup CMake build directory:
    

```
mkdir build
cd build   
  ```  
    
#### 改成
\\wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\RP2040MacropadHidSample\src\build\CMakeCache.txt   
`export PICO_SDK_PATH=../../../../../../pico/pico-sdk`    
    
### 要先更新 hid.h 和 hid_device.h
    
    
```
cmake -DPICO_BOARD=adafruit_macropad_rp2040 ..
```
    
    
```
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ cmake -DPICO_BOARD=adafruit_macropad_rp2040 ..
PICO_SDK_PATH is /home/ab/pico/pico-sdk
Defaulting PICO_PLATFORM to rp2040 since not specified.
Defaulting PICO platform compiler to pico_arm_gcc since not specified.
-- Defaulting build type to 'Release' since not specified.
PICO compiler is pico_arm_gcc
-- The C compiler identification is GNU 10.3.1
-- The CXX compiler identification is GNU 10.3.1
-- The ASM compiler identification is GNU
-- Found assembler: /usr/bin/arm-none-eabi-gcc
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/arm-none-eabi-gcc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/arm-none-eabi-g++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
Build type is Release
PICO target board is adafruit_macropad_rp2040.
Using board configuration from /home/ab/pico/pico-sdk/src/boards/include/boards/adafruit_macropad_rp2040.h
-- Found Python3: /usr/bin/python3.10 (found version "3.10.6") found components: Interpreter
TinyUSB available at /home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040; enabling build support for USB.
BTstack available at /home/ab/pico/pico-sdk/lib/btstack
cyw43-driver available at /home/ab/pico/pico-sdk/lib/cyw43-driver
Pico W Bluetooth build support available.
lwIP available at /home/ab/pico/pico-sdk/lib/lwip
mbedtls available at /home/ab/pico/pico-sdk/lib/mbedtls
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ab/pico/pico-examples/build/RP2040MacropadHidSample/src/build
ab@DESKTOP-BLKOVOI:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$
```    
    
    
    
    

請注意，如果步驟 3 中尚未設定 PICO_SDK_PATH 環境變量，-DPICO_SDK_PATH=則還需要指定。
Note, if PICO_SDK_PATH environment variable has not been set up in step 3, -DPICO_SDK_PATH= will need to be specified as well.

    
    
8. 從專案建置目錄中建立您的目標。
   Make your target from the project build directory.
`make`

    
9. 在 Macropad 上，按住旋轉編碼器按鈕的同時，按下板左側 OLED 螢幕正下方的重設按鈕。Macropad 設備應顯示為可移動設備RPI-RP2 (DriveLetter:)
   On the Macropad, while holding down the rotary encoder button, press the reset button on the left side of the board, right under the OLED screen. Macropad device should show up as a removable device RPI-RP2 (DriveLetter:)
10. 開啟建置目錄的資源管理器窗口，並將 Macropad.uf2 複製到 Macropad 可移動裝置。設備應自動刪除並重新啟動。
    Open an Explorer window to the build directory, and copy macropad.uf2 to the Macropad removeable device. Device should automatically remove itself and reboot.
11. 開啟“設定”>“個人化”>“動態照明”，然後看到裝置出現。
    Open Settings > Personalization > Dynamic Lighting, and see the device come up.

============================================================

### 更新 hid.h 和 hid_device.h
C:\Users\C940\Desktop\tinyusb-hid-lighting\src\class\hid

將頭檔 hid.h 和 hid_device.h 複製到 Pico SDK 路徑中的 TinyUSB 庫，即 <PicoSdkRoot>/lib/tinyusb/src/class/hid/

\\wsl.localhost\Ubuntu\home\ab\pico\pico-sdk\lib\tinyusb\src\class\hid



============================================================

=================================
### cmake 路徑問題
//Path to the Raspberry Pi Pico SDKPICO_SDK_PATH:PATH=../../pico-sdk
PICO_SDK_PATH:PATH=../../../../../../pico/pico-sdk

=================================


[100%] Built target picow_bt_example_pan_lwip_http_server_background
ab@C940-PC:~/pico/pico-examples/build/pico_w$ ls
CMakeFiles  Makefile  blink  bt  cmake_install.cmake  wifi
ab@C940-PC:~/pico/pico-examples/build/pico_w$ cd blink/
ab@C940-PC:~/pico/pico-examples/build/pico_w/blink$ ls
CMakeLists.txt  blink.c
ab@C940-PC:~/pico/pico-examples/build/pico_w/blink$ make
make: *** No targets specified and no makefile found.  Stop.
ab@C940-PC:~/pico/pico-examples/build/pico_w/blink$ cd ..
ab@C940-PC:~/pico/pico-examples/build/pico_w$ ls
CMakeFiles  Makefile  blink  bt  cmake_install.cmake  wifi
ab@C940-PC:~/pico/pico-examples/build/pico_w$ cd blink/
ab@C940-PC:~/pico/pico-examples/build/pico_w/blink$ ls
CMakeLists.txt  blink.c
ab@C940-PC:~/pico/pico-examples/build/pico_w/blink$ cd ..
ab@C940-PC:~/pico/pico-examples/build/pico_w$ cd ..
ab@C940-PC:~/pico/pico-examples/build$ cd blink/
ab@C940-PC:~/pico/pico-examples/build/blink$ ls
CMakeFiles  CMakeLists.txt  Makefile  blink.c  cmake_install.cmake  elf2uf2
    
`ab@C940-PC:~/pico/pico-examples/build/blink$ make`
    
```
Performing build step for 'ELF2UF2Build'
Consolidate compiler generated dependencies of target elf2uf2
[100%] Built target elf2uf2
No install step for 'ELF2UF2Build'
Completed 'ELF2UF2Build'
Built target ELF2UF2Build
Built target bs2_default
Built target bs2_default_padded_checksummed_asm
Scanning dependencies of target blink
Building C object blink/CMakeFiles/blink.dir/blink.c.obj
/home/ab/pico/pico-examples/blink/blink.c: In function 'main':
/home/ab/pico/pico-examples/blink/blink.c:11:2: warning: #warning blink example requires a board with a regular LED [-Wcpp]
   11 | #warning blink example requires a board with a regular LED
      |  ^~~~~~~
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdlib/stdlib.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_gpio/gpio.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_platform/platform.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_claim/claim.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_sync/sync.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_irq/irq.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_irq/irq_handler_chain.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_sync/sem.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_sync/lock_core.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_sync/mutex.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_sync/critical_section.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_time/time.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_time/timeout_helper.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_timer/timer.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_util/datetime.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_util/pheap.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/common/pico_util/queue.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_uart/uart.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_clocks/clocks.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_pll/pll.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_vreg/vreg.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_watchdog/watchdog.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_xosc/xosc.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_divider/divider.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_runtime/runtime.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_printf/printf.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_bit_ops/bit_ops_aeabi.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_bootrom/bootrom.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_divider/divider.S.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_aeabi.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_init_rom.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_math.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_v1_rom_shim.S.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_int64_ops/pico_int64_ops_aeabi.S.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_aeabi.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_init_rom.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_math.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_v1_rom_shim.S.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_malloc/pico_malloc.c.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_mem_ops/mem_ops_aeabi.S.obj
Building ASM object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/crt0.S.obj
Building CXX object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/new_delete.cpp.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/binary_info.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio/stdio.c.obj
Building C object blink/CMakeFiles/blink.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_uart/stdio_uart.c.obj
Linking CXX executable blink.elf
Built target blink
```

### 克隆官網程式
`ab@C940-PC:~/pico/pico-examples/build/blink$ cd ..`

`ab@C940-PC:~/pico/pico-examples/build$ git clone https://github.com/microsoft/RP2040MacropadHidSample.git`

```
Cloning into 'RP2040MacropadHidSample'...
remote: Enumerating objects: 78, done.
remote: Counting objects: 100% (78/78), done.
remote: Compressing objects: 100% (59/59), done.
remote: Total 78 (delta 33), reused 49 (delta 17), pack-reused 0
Receiving objects: 100% (78/78), 5.61 MiB | 10.75 MiB/s, done.
Resolving deltas: 100% (33/33), done.
ab@C940-PC:~/pico/pico-examples/build$ sudo apt install build-essential
[sudo] password for ab:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
build-essential is already the newest version (12.9ubuntu3).
0 upgraded, 0 newly installed, 0 to remove and 45 not upgraded.
```
    
`ab@C940-PC:~/pico/pico-examples/build$ git submodule update --init`
    
```
ab@C940-PC:~/pico/pico-examples/build$ ls
CMakeCache.txt           adc     cmake_install.cmake  flash        i2c        pico_w     pwm    system  watchdog
CMakeFiles               blink   divider              generated    interp     picoboard  reset  timer
Makefile                 clocks  dma                  gpio         multicore  pio        rtc    uart
RP2040MacropadHidSample  cmake   elf2uf2              hello_world  pico-sdk   pioasm     spi    usb
```

    
    
```
ab@C940-PC:~/pico/pico-examples/build$ cd RP2040MacropadHidSample/
ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample$ cd src/
ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src$ mkdir build
ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src$ cd build
```

### cmake PICO_SDK_PATH 路徑問題
//Path to the Raspberry Pi Pico SDKPICO_SDK_PATH:PATH=../../pico-sdk
PICO_SDK_PATH:PATH=../../../../../../pico/pico-sdk

```
ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ cmake -DPICO_BOARD=adafruit_macropad_rp2040 ..
Using PICO_SDK_PATH from environment ('../../pico-sdk/')
CMake Error at pico_sdk_import.cmake:63 (message):
Directory '/home/ab/pico/pico-examples/build/RP2040MacropadHidSample/pico-sdk' not found
Call Stack (most recent call first):
CMakeLists.txt:3 (include)
-- Configuring incomplete, errors occurred!
```


============================================================

\\wsl.localhost\Ubuntu\home\ab\pico\pico-sdk

ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$


//Path to the Raspberry Pi Pico SDKPICO_SDK_PATH:PATH=../../pico-sdk
PICO_SDK_PATH:PATH=../../../../../../pico/pico-sdk

============================================================

### cmake 成功

`ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ cmake -DPICO_BOARD=adafruit_macropad_rp2040 ..`
    
    
```
PICO_SDK_PATH is /home/ab/pico/pico-sdk
Defaulting PICO_PLATFORM to rp2040 since not specified.
Defaulting PICO platform compiler to pico_arm_gcc since not specified.
-- Defaulting build type to 'Release' since not specified.
PICO compiler is pico_arm_gcc
-- The C compiler identification is GNU 10.3.1
-- The CXX compiler identification is GNU 10.3.1
-- The ASM compiler identification is GNU
-- Found assembler: /usr/bin/arm-none-eabi-gcc
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/arm-none-eabi-gcc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/arm-none-eabi-g++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
Build type is Release
PICO target board is adafruit_macropad_rp2040.
Using board configuration from /home/ab/pico/pico-sdk/src/boards/include/boards/adafruit_macropad_rp2040.h
-- Found Python3: /usr/bin/python3.10 (found version "3.10.12") found components: Interpreter
TinyUSB available at /home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040; enabling build support for USB.
BTstack available at /home/ab/pico/pico-sdk/lib/btstack
cyw43-driver available at /home/ab/pico/pico-sdk/lib/cyw43-driver
Pico W Bluetooth build support available.
lwIP available at /home/ab/pico/pico-sdk/lib/lwip
mbedtls available at /home/ab/pico/pico-sdk/lib/mbedtls
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ab/pico/pico-examples/build/RP2040MacropadHidSample/src/build
    
```
    
    
`ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$`




============================================================


C:\Users\C940\Desktop\tinyusb-hid-lighting\src\class\hid

將頭檔 hid.h 和 hid_device.h 複製到 Pico SDK 路徑中的 TinyUSB 庫，即<PicoSdkRoot>/lib/tinyusb/src/class/hid/

\\wsl.localhost\Ubuntu\home\ab\pico\pico-sdk\lib\tinyusb\src\class\hid


    

============================================================
### make 出錯是 hid.h 和 hid_device.h 造成
    
`ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ make`
    
```
Scanning dependencies of target bs2_default
[  2%] Built target bs2_default
[  4%] Built target bs2_default_padded_checksummed_asm
[  5%] Performing build step for 'PioasmBuild'
Consolidate compiler generated dependencies of target pioasm
[100%] Built target pioasm
[  6%] No install step for 'PioasmBuild'
[  7%] Completed 'PioasmBuild'
[ 12%] Built target PioasmBuild
[ 13%] Built target macropad_neopixel_pio_h
[ 14%] Performing build step for 'ELF2UF2Build'
Consolidate compiler generated dependencies of target elf2uf2
[100%] Built target elf2uf2
[ 15%] No install step for 'ELF2UF2Build'
[ 15%] Completed 'ELF2UF2Build'
[ 20%] Built target ELF2UF2Build
Scanning dependencies of target macropad
Consolidate compiler generated dependencies of target macropad
[ 21%] Building C object CMakeFiles/macropad.dir/usb_descriptors.c.obj
/home/ab/pico/pico-examples/build/RP2040MacropadHidSample/src/usb_descriptors.c:76:5: warning: implicit declaration of function 'TUD_HID_REPORT_DESC_LIGHTING'; did you mean 'TUD_HID_REPORT_DESC_FIDO_U2F'? [-Wimplicit-function-declaration]
   76 |     TUD_HID_REPORT_DESC_LIGHTING( REPORT_ID_LIGHTING_LAMP_ARRAY_ATTRIBUTES )
      |     ^~~~~~~~~~~~~~~~~~~~~~~~~~~~
      |     TUD_HID_REPORT_DESC_FIDO_U2F
/home/ab/pico/pico-examples/build/RP2040MacropadHidSample/src/usb_descriptors.c:76:5: error: initializer element is not constant
/home/ab/pico/pico-examples/build/RP2040MacropadHidSample/src/usb_descriptors.c:76:5: note: (near initialization for 'desc_hid_report[67]')
make[2]: *** [CMakeFiles/macropad.dir/build.make:90: CMakeFiles/macropad.dir/usb_descriptors.c.obj] Error 1
make[1]: *** [CMakeFiles/Makefile2:1511: CMakeFiles/macropad.dir/all] Error 2
make: *** [Makefile:91: all] Error 2
ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ cmake -DPICO_BOARD=adafruit_macropad_rp2040 ..
PICO_SDK_PATH is /home/ab/pico/pico-sdk
PICO platform is rp2040.
Build type is Release
PICO target board is adafruit_macropad_rp2040.
Using board configuration from /home/ab/pico/pico-sdk/src/boards/include/boards/adafruit_macropad_rp2040.h
TinyUSB available at /home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040; enabling build support for USB.
BTstack available at /home/ab/pico/pico-sdk/lib/btstack
cyw43-driver available at /home/ab/pico/pico-sdk/lib/cyw43-driver
Pico W Bluetooth build support available.
lwIP available at /home/ab/pico/pico-sdk/lib/lwip
mbedtls available at /home/ab/pico/pico-sdk/lib/mbedtls
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ab/pico/pico-examples/build/RP2040MacropadHidSample/src/build
```
    
####又錯

    
    
    
    
    
    
    
    
`ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$ make`

    
```
Scanning dependencies of target bs2_default
[  2%] Built target bs2_default
[  4%] Built target bs2_default_padded_checksummed_asm
[  5%] Performing build step for 'PioasmBuild'
[100%] Built target pioasm
[  6%] No install step for 'PioasmBuild'
[  7%] Completed 'PioasmBuild'
[ 12%] Built target PioasmBuild
[ 13%] Built target macropad_neopixel_pio_h
[ 14%] Performing build step for 'ELF2UF2Build'
[100%] Built target elf2uf2
[ 15%] No install step for 'ELF2UF2Build'
[ 15%] Completed 'ELF2UF2Build'
[ 20%] Built target ELF2UF2Build
Scanning dependencies of target macropad
Consolidate compiler generated dependencies of target macropad
[ 21%] Building C object CMakeFiles/macropad.dir/usb_descriptors.c.obj
[ 22%] Building C object CMakeFiles/macropad.dir/Keys/Keys.c.obj
[ 23%] Building C object CMakeFiles/macropad.dir/Encoder/Encoder.c.obj
[ 24%] Building C object CMakeFiles/macropad.dir/Lighting/Neopixel.c.obj
[ 25%] Building C object CMakeFiles/macropad.dir/Lighting/LampArray.c.obj
[ 26%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdlib/stdlib.c.obj
[ 27%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_gpio/gpio.c.obj
[ 28%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_platform/platform.c.obj
[ 29%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_claim/claim.c.obj
[ 30%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_sync/sync.c.obj
[ 31%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_irq/irq.c.obj
[ 32%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_irq/irq_handler_chain.S.obj
[ 33%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_sync/sem.c.obj
[ 34%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_sync/lock_core.c.obj
[ 35%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_sync/mutex.c.obj
[ 36%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_sync/critical_section.c.obj
[ 37%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_time/time.c.obj
[ 38%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_time/timeout_helper.c.obj
[ 39%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_timer/timer.c.obj
[ 40%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_util/datetime.c.obj
[ 41%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_util/pheap.c.obj
[ 42%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/common/pico_util/queue.c.obj
[ 43%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_uart/uart.c.obj
[ 44%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_clocks/clocks.c.obj
[ 45%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_pll/pll.c.obj
[ 46%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_vreg/vreg.c.obj
[ 47%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_watchdog/watchdog.c.obj
[ 48%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_xosc/xosc.c.obj
[ 48%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_divider/divider.S.obj
[ 50%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_runtime/runtime.c.obj
[ 51%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_printf/printf.c.obj
[ 52%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_bit_ops/bit_ops_aeabi.S.obj
[ 53%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_bootrom/bootrom.c.obj
[ 54%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_divider/divider.S.obj
[ 55%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_aeabi.S.obj
[ 56%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_init_rom.c.obj
[ 57%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_math.c.obj
[ 58%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_double/double_v1_rom_shim.S.obj
[ 59%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_int64_ops/pico_int64_ops_aeabi.S.obj
[ 60%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_aeabi.S.obj
[ 61%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_init_rom.c.obj
[ 62%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_math.c.obj
[ 63%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_float/float_v1_rom_shim.S.obj
[ 64%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_malloc/pico_malloc.c.obj
[ 65%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_mem_ops/mem_ops_aeabi.S.obj
[ 66%] Building ASM object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/crt0.S.obj
[ 67%] Building CXX object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/new_delete.cpp.obj
[ 68%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_standard_link/binary_info.c.obj
[ 69%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio/stdio.c.obj
[ 70%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_uart/stdio_uart.c.obj
[ 71%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_usb/reset_interface.c.obj
[ 72%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_usb/stdio_usb.c.obj
[ 73%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_stdio_usb/stdio_usb_descriptors.c.obj
[ 74%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_unique_id/unique_id.c.obj
[ 75%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_flash/flash.c.obj
[ 76%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040/dcd_rp2040.c.obj
[ 77%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/portable/raspberrypi/rp2040/rp2040_usb.c.obj
[ 78%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/device/usbd.c.obj
[ 79%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/device/usbd_control.c.obj
[ 80%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/audio/audio_device.c.obj
[ 81%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/cdc/cdc_device.c.obj
[ 82%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/dfu/dfu_device.c.obj
[ 83%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/dfu/dfu_rt_device.c.obj
[ 84%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/hid/hid_device.c.obj
[ 85%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/midi/midi_device.c.obj
[ 86%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/msc/msc_device.c.obj
[ 87%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/net/ecm_rndis_device.c.obj
[ 88%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/net/ncm_device.c.obj
[ 89%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/usbtmc/usbtmc_device.c.obj
[ 90%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/vendor/vendor_device.c.obj
[ 91%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/class/video/video_device.c.obj
[ 92%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/tusb.c.obj
[ 93%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/src/common/tusb_fifo.c.obj
[ 94%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_fix/rp2040_usb_device_enumeration/rp2040_usb_device_enumeration.c.obj
[ 95%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/pico_multicore/multicore.c.obj
[ 96%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/src/rp2_common/hardware_pio/pio.c.obj
[ 97%] Building C object CMakeFiles/macropad.dir/home/ab/pico/pico-sdk/lib/tinyusb/hw/bsp/rp2040/family.c.obj
[ 98%] Linking CXX executable macropad.elf
[100%] Built target macropad
```
    
`ab@C940-PC:~/pico/pico-examples/build/RP2040MacropadHidSample/src/build$`

### 得到 macropad.uf2
\\wsl.localhost\Ubuntu\home\ab\pico\pico-examples\build\RP2040MacropadHidSample\src\build
macropad.uf2

