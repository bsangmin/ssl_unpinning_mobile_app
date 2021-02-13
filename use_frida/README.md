# Using Frida

### Install and run Frida server on devices

Get your Frida server at https://github.com/frida/frida/releases  
You should download frida-server-{version}-android-{bit} or {type}.xz for android

```
:version
what you want

:bit
$ adb shell getprop ro.product.cpu.abi
ex) x86

:type
$ adb shell getprop ro.product.cpu.abi2
ex) arm
```

In my case frida-server-14.2.12-android-x86.xz

```bash
$ tar -xvf frida-server-14.2.12-android-x86.xz
$ adb push frida-server-14.2.12-android-x86 /data/local/tmp
$ adb shell

adb $ cd /data/local/tmp
adb $ mv frida-server-14.2.12-android-x86 frida_srv (if you need)
adb $ chmod 744 frida_srv
adb $ ./frida_srv &
```

### Frida tool install

You can install from npm or pip  
See detail https://frida.re/

```bash
$ pip install frida-tools
```

### Unpinning

```bash
$ frida-ps -Uai

 PID  Name                                   Identifier
----  -------------------------------------  -----------------------------------------
2442  Android Services Library               android.ext.services
2124  Android System                         android
2490  Blocked Numbers Storage                com.android.providers.blockednumber
3171  Bookmark Provider                      com.android.bookmarkprovider
3119  Browser                                com.android.browser
2752  Calendar Storage                       com.android.providers.calendar
2124  Call Management                        com.android.server.telecom
...

$ frida -U --codeshare masbog/frida-android-unpinning-ssl "com.android.browser"
     ____
    / _  |   Frida 14.2.12 - A world-class dynamic instrumentation toolkit
   | (_| |
    > _  |   Commands:
   /_/ |_|       help      -> Displays the help system
   . . . .       object?   -> Display information about 'object'
   . . . .       exit/quit -> Exit
   . . . .
   . . . .   More info at https://www.frida.re/docs/home/
Attaching...

[.] Android Cert Pinning Bypass
[.] TrustManagerImpl Android 7+ detection...
[-] TrustManagerImpl Not Found
[.] TrustManager Android < 7 detection...
[.] OkHTTP 3.x detection...
[-] OkHTTP 3.x Not Found
[.] Appcelerator Titanium detection...
[-] Appcelerator Titanium Not Found
...
```
