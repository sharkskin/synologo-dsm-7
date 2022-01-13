[来自于Izumiko/redpill-loader-action](https://github.com/Izumiko/redpill-loader-action)

# 用Github的Actions编译RedPill的引导程序

DS918+ 和 DS3615xs 群晖7.0.1引导程序

使用方法：
fock仓库以后，修改user_config.DS918+.json配置文件
代码:

#{
#  "extra_cmdline": {
#    "vid": "0xABAB",
#    "pid": "0xABAB",
#    "sn": "125XXXX",
#    "netif_num":"2",
#    "mac1": "0011XXXX",
#    "mac2": "0011XXXX"
#    },
#    "synoinfo": {
#    "maxdisks" : "16",
#    "internalportcfg" : "0xf006",
#    "esataportcfg" : "0x0ff9"
#    },
#    "ramdisk_copy": {},
#    "extensions": []
#}

1，根据引导U盘设置PID VID；
2，双网卡"netif_num":"2",并且有两个MAC号码，单网卡netif_num=1，Mac设置一个就行；
3，internalportcfg，esataportcfg的配置见解决DSM7关于esata的问题
4，编译完成后，用Rufus写入引导U盘，物理机开机时注意GNU GRUB默认USB引导就可以
5，开机

关于关机命令支持：
关机键驱动
官方引导和大家发出来的引导一般都不支持关机操作，包括物理机关机键和虚拟机关机键，这是因为缺少了acpi的驱动，
引导编译中在build-ds918-7.0.1.sh的
# build redpill-load部分需要增加一行添加驱动指令（./ext-manager.sh add……那一行）：
##代码:
##cd redpill-load
##cp ${root}/user_config.DS918+.json ./user_config.json
##./ext-manager.sh add https://raw.githubusercontent.com/jumkey/redpill-load/develop/redpill-acpid/rpext-index.json
##sudo ./build-loader.sh 'DS918+' '7.0.1-42218'
