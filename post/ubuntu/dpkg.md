
## Ubuntu 下如何查看已安装的软件

### 1.查看安装的所有软件

```
dpkg -l      
```
例如：`dpkg -l | grep ftp`

### 2.查看软件安装的路径
```
dpkg -L | grep ftp
```
也可以用 `whereis ftp`

### 3.查看软件版本
```
aptitude show
```
例如：`aptitude  show ftp`