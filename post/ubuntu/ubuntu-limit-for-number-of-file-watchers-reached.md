系统对文件监控的数量已经到达限制数量了

```
Ubuntu Error: ENOSPC:System limit for number of file watchers reached
```

解决方法：

修改系统监控文件数量

Ubuntu

```bash
sudo gedit /etc/sysctl.conf
```

添加一行在最下面.

```bash
fs.inotify.max_user_watches=524288
```

然后保存退出！

执行

```bash
sudo sysctl -p
```

然后就解决了！