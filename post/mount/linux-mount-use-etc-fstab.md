Linux自动挂载（配置/etc/fatab）

# mount 中的第三个参数，硬盘类型，到底写什么呢？

## （错误）根据 mount 命令

```
ubuntu@utuntu:~$ mount | grep sda
/dev/sda2 on /boot type ext4 (rw,relatime,data=ordered)
/dev/sda1 on /boot/efi type vfat (rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro)
ubuntu@utuntu:~$ mount | grep sdb
/dev/sdb1 on /home/ubuntu/sdb type fuseblk (rw,relatime,user_id=0,group_id=0,allow_other,blksize=4096)
```

/etc/fstab 中应该这样写

```
/dev/sdb1	/home/ubuntu/sdb	fuseblk	defaults 0 0
```

## 根据 blkid 命令

```
ubuntu@utuntu:~$ blkid 
/dev/sda1: UUID="B4CB-FC05" TYPE="vfat" PARTUUID="54870ae6-8ccc-44c3-b600-34a116fffe23"
/dev/sda2: UUID="90b2a4b2-a3b1-4640-afb7-1d63314a8a26" TYPE="ext4" PARTUUID="1fc077e0-3aa8-498d-b40f-b7e4e4a01250"
/dev/sda3: UUID="0oTOy6-cSKq-fYhr-XMTV-za8S-WArh-Cusj81" TYPE="LVM2_member" PARTUUID="c75bca25-afe2-4859-8b81-e9dfe42842d7"
/dev/sdb1: UUID="FE46843C4683F3A5" TYPE="ntfs" PARTUUID="b753b753-01"
/dev/mapper/ubuntu--vg-ubuntu--lv: UUID="cfb4d330-2a62-4b62-b7c0-7ed708ac224a" TYPE="xfs"
ubuntu@utuntu:~$ cat /etc/fstab 
UUID=cfb4d330-2a62-4b62-b7c0-7ed708ac224a / xfs defaults 0 0
UUID=90b2a4b2-a3b1-4640-afb7-1d63314a8a26 /boot ext4 defaults 0 0
UUID=B4CB-FC05 /boot/efi vfat defaults 0 0
/swap.img	none	swap	sw	0	0
ubuntu@utuntu:~$ 
```

/etc/fstab 中应该这样写

```
/dev/sdb1	/home/ubuntu/sdb	ntfs	defaults 0 0
```



https://www.cnblogs.com/miaoxg/p/5971036.html
https://blog.csdn.net/greenapple_shan/article/details/52799631

知道了，应该写 ntfs 哟。