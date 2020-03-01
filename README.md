设置完之后，以后源码有更新只需要点一下就能自动编译了。

编译时间大概是20-30分钟左右，不同型号的固件时间不同。

Github Actions全自动编译Padavan固件登录信息
源码的登录IP：192.168.2.1
用户名/密码：admin/admin
wifi密码:1234567890

Github Actions全自动编译Padavan固件教程
1.首先打开

https://github.com/chongshengB/Padavan-build

（如果是手机访问的请把页面拉到最底部，然后切换到Desktop version）

2.然后点击右上角的Fork按钮fork源码到你的github，如果没登录github帐号跳转到登录界面。

3.修改：.github/workflows/build-padavan.yml文件中：（此文件克隆的是本人的Padavan源码https://github.com/chongshengB/rt-n56u）

- name: Build Firmware
      env:
        TNAME: K2P-5.0（把K2P-5.0改成你需要编译的型号）

4.文件中有部分插件的选项，请按需修改需要集成哪些插件，文件中都有注释。如下修改build-padavan.yml文件中的代码，自定义固件编译的功能。

#以下选项是定义你需要的功能（y=集成,n=忽略），重新写入到.config文件
       ######################################################################    
       echo "CONFIG_FIRMWARE_INCLUDE_MENTOHUST=n" >> .config #MENTOHUST    
       echo "CONFIG_FIRMWARE_INCLUDE_SCUTCLIENT=n" >> .config #SCUTCLIENT    
       echo "CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS=y" >> .config #SS plus+    
       echo "CONFIG_FIRMWARE_INCLUDE_SSSERVER=n" >> .config #SS server    
       echo "CONFIG_FIRMWARE_INCLUDE_DNSFORWARDER=n" >> .config #DNSFORWARDER    
       echo "CONFIG_FIRMWARE_INCLUDE_ADBYBY=y" >> .config #adbyby plus+    
       echo "CONFIG_FIRMWARE_INCLUDE_FRPC=n" >> .config #内网穿透FRPC    
       echo "CONFIG_FIRMWARE_INCLUDE_FRPS=n" >> .config #内网穿透FRPS    
       echo "CONFIG_FIRMWARE_INCLUDE_TUNSAFE=n" >> .config #TUNSAFE    
       echo "CONFIG_FIRMWARE_INCLUDE_ALIDDNS=y" >> .config #阿里DDNS    
       echo "CONFIG_FIRMWARE_INCLUDE_SMARTDNS=y" >> .config #smartdns    
       echo "CONFIG_FIRMWARE_INCLUDE_SMARTDNSBIN=y" >> .config #smartdns二进制文件    
       echo "CONFIG_FIRMWARE_INCLUDE_V2RAY=n" >> .config #集成v2ray执行文件，如果不集成，会从网上下载下来执行，不影响正常使用    
       echo "CONFIG_FIRMWARE_INCLUDE_TROJAN=n" >> .config #集成trojan执行文件，如果不集成，会从网上下载下来执行，不影响正常使用    
       echo "CONFIG_FIRMWARE_INCLUDE_KOOLPROXY=y" >> .config #KP广告过滤    
       echo "CONFIG_FIRMWARE_INCLUDE_CADDY=y" >> .config #在线文件管理服务    
       echo "CONFIG_FIRMWARE_INCLUDE_CADDYBIN=n" >> .config #集成caddu执行文件，此文件有13M,请注意固件大小。如果不集成，会从网上下载下来执行，不影响正常使用    
       echo "CONFIG_FIRMWARE_INCLUDE_KUMASOCKS=y" >> .config    
       echo "CONFIG_FIRMWARE_INCLUDE_ADGUARDHOME=y" >> .config
5.接着新建一个Releases，然后点击Actions，就会看到有一个Build Padavan的任务在运行，如下图：

利用Github全自动编译Padavan固件

6.完成之后前面黄色圈会变成绿色勾，如果显示红色交叉就代表出现错误。

7.编译完成后点击Build Padavan,然后点击右上角的：Artifacts就可以下载编译好的文件。
