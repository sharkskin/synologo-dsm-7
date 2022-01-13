[来自于Izumiko/redpill-loader-action](https://github.com/Izumiko/redpill-loader-action)

# 用Github的Actions编译RedPill的引导程序

DS918+ 和 DS3615xs 群晖7.0.1引导程序

使用方法：
fock仓库以后，修改user_config.DS918+.json配置文件
代码:

{
  "extra_cmdline": {
    "vid": "0xABAB",
    "pid": "0xABAB",
    "sn": "125XXXX",
    "netif_num":"2",
    "mac1": "0011XXXX",
    "mac2": "0011XXXX"
    },
    "synoinfo": {
    "maxdisks" : "16",
    "internalportcfg" : "0xf006",
    "esataportcfg" : "0x0ff9"
    },
    "ramdisk_copy": {},
    "extensions": []
}

1，根据引导U盘设置PID VID；
2，双网卡"netif_num":"2",并且有两个MAC号码，单网卡netif_num=1，Mac设置一个就行；
3，internalportcfg，esataportcfg的配置见解决DSM7关于esata的问题
如果已经装了42218，不管硬盘在哪个盘位，编译好的引导盘应该都能正确引导，只要放在internalportcfg对应的盘位就行，不必放在1、2盘位，也不需要设置satamap，diskmap；
4，编译完成后，用Rufus写入引导U盘，物理机开机时注意GNU GRUB默认USB引导就可以。
这里一个插曲，由于我原来用虚拟机的虚拟盘引导，开机需要选SATA，开始时物理机选择SATA引导就无法启动。下文中DSM安装开在55%~59%一般也是引导方式选择错误、VID PID设置错误或者启动U盘本身问题造成的。
5，插腚~开机~
