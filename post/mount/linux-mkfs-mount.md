umount后格式化后mount

## umount

```bash
ubuntu@utuntu:~$ sudo umount sdb
```

### umount - target is busy

https://www.cnblogs.com/ding2016/p/9605526.html

```bash
ubuntu@utuntu:~$ sudo umount sdb
umount: /home/ubuntu/sdb: target is busy.
ubuntu@utuntu:~$ mount | grep sdb
/dev/sdb1 on /home/ubuntu/sdb type fuseblk (rw,relatime,user_id=0,group_id=0,allow_other,blksize=4096)
ubuntu@utuntu:~$ which fuser
/bin/fuser
ubuntu@utuntu:~$ fuser -mv sdb
                     USER        PID ACCESS COMMAND
/home/ubuntu/sdb:    root     kernel mount /home/ubuntu/sdb
                     ubuntu    17228 ..c.. node
ubuntu@utuntu:~$ sudo kill 17228
ubuntu@utuntu:~$ sudo umount sdb
ubuntu@utuntu:~$ ls sdb
ubuntu@utuntu:~$ 
```

## 格式化分区（mkfs.ext4） 

对新建分区（例：/dev/sda1）进行格式化：mkfs.ext4 /dev/sdb1

把/dev/sdb1格式化成ext4文件系统。

```bash
# mkfs -t ext4 /dev/sdb1
```

## 挂载

```bash
mkdir /sdb 
sudo mount /dev/sdb1 /sdb
```

## 写入 fstab

```bash
ubuntu@utuntu:~$ sudo vi /etc/fstab 
ubuntu@utuntu:~/lcnx/local$ cat /etc/fstab | grep sdb
/dev/sdb1	/sdb	fuseblk	defaults 0 0
ubuntu@utuntu:~/lcnx/local$ 
```