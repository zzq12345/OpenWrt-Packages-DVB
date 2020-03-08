1、进入lede编译主目录，cd package 
2、git clone https://github.com/kob/OpenWrt-Packages-DVB.git
3、rm -rf  ./feeds/packages/multimedia/tvheadend #删除原来自带的tvheadend插件
4、make menuconfig  进入菜单 选择DVB-EXTRAS 进去选择tvheadend #默认依赖libdvbcsa会自动选中
5、make -j1 V=s 编译即可  
6、如果出现ERROR: Failed to fetch dvb-scan files (use --disable-dvbscan to skip)错误，请运行sudo apt-get install dvb-apps
   或者修改OpenWrt-Packages-DVB/tvheadend下的Makefile文件，在第49行后面回车并加入
   --disable-dvbscan \ 
   --disable-bintray_cache  \ 
   
