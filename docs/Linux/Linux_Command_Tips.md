# Linux Command Tips

- 查找指定目录名所在路径

```linux
find / -name '*ebapps' -type d
```

- dos2unix *.sh

将当前目录下的所有.sh文件转换为Unix编码格式，特别是从Windows传过来的脚本有\r符号，Linux不认

- 在指定目录下递归查找带有特定字符（此处为update，没有引号）的文件，并打印出该字符串所在行的内容

```linux
grep -r update /etc/acpi
```

- 反向查找，在文件名符合*somefile*的文件中，查找不包含str的文件

```linux
grep -v str *somefile*
```

- 获取当前时间yyyyMMdd

```linux
date "+%Y%m%d"
```

- 时间日期格式转换

```linux
date --date="Dec 14, 2021" "+%Y%m%d"
date --date="Tuesday, July 13, 2021" "+%Y%m%d"
date -d "Jun 29, 2021" +"%Y"
date -d "Jun 29, 2021" +"%m"
date -d "Jun 29, 2021" +"%d"
```

- 找到指定日期前一个月（日，年等）的日期

```linux
date -d "20000131 1 month ago" "+%Y%m%d"
(19991231)
```

- Linux权限
- user(u), group(g), others(o)三种角色，修改权限

```linux
chmod u=rwx[,g,o] file
chmod u-r,u+w file/dir
chmod -R a=rwx dir # dir目录下都设置rwx权限
```

- eg:drw-r--wx
当前属性是目录，user的权限是rw-(110),group的权限是r--(100),others的权限是-wx(011)
目标类型，有目录（用'd'表示），有文件（用'-'表示），有连接文件（用'l'表示）
八进制表示的三个基数是4（read），2（write），1（execute），111就是三个角色都赋予execute权限，222就是
三个角色都设置写的权限，333就是三个角色都设置2+1写权限和执行权限，444就是三个角色都设置读权限，555就是
4+1，666就二十4+2，777就是4+2+1
注意：chmod相当于重置并设置，如设置权限之前，aaa的权限是d-wx-wx-wx，执行chmod 444 aaa之后为dr--r--r--。
需要加权限使用chmod a+r aaa

- root用户可以```读写权限，root用户无执行权限也是无法执行，但是可以给自身添加上权限

- 给opt目录重新以只读/可读写的模式挂载

```linux
mount -o remount,ro /opt
mount -o remount,rw /opt
```

- 文件有权限，但是即使是root还是不能写，可能是文件被设置了不可用修改属性

```linux
chattr +i /opt
chattr -i /opt
```

- 指定目录下的文件（-type f）都转化为Unix格式

```linux
find /home/username/script/ -type f | xargs dos2unix
```

- 替换文件中的字符串

```linux
sed -ri 's/(KeyPrefix = ")[^"]*/\122.22.22.190/' aaa.txt
值有引号才能yong，[^"]为最后的限定引号，如果值没有引号或其他指定的字符，则连同【KeyPrefix = 】全部
替换为22.22.22.190，122.的第一个1作为标识符会被切掉，但是不可或缺，其他符号一样的，比如`，会被替换
掉``中间的字符

sed -ri 's/(KeyPrefix = aa.)[^\s]*/\1yyyy/' test.dat 
没有引号KeyPrefix = aa.xxxx被替换为KeyPrefix = aa.yyyy，注意yyyy前的1

sed -ri 's/(xxxx=)[^=]*[`$]/\1"aaa=11,bbb=15"/' cccc.sh
替换cccc.sh中的xxxx=`echo xxxx`为xxxx="aaa=11,bbb=15"
```

- 匹配多个关键字所在行，并且排除有#号的（一般是注释）

```linux
cat config.dat | grep -v '#' | grep -E "aa|vv|cc|dd|ee"
```

- 场景：前缀固定，后缀不确定如日期时间，可以统一命名，解压命令就可以固定写

```linux
mv aaa*.zip aaa.zip
# 解压且覆盖(-o)到目录(-d)aaaa，可以多次执行，-q：静默解压不显示信息
unzip -qo aaa.zip -d aaaa/
```

- 只列举目录

```linux
ls -l | grep '^d'
ls -lF | grep "/$"
ls -l | grep "^d" |grep -E "ping\-pong_[0-9]\.[0-9]+\.[0-9]+"
```

- 由空格分隔，拿到最后一列

```linux
ls -l | grep "^d" |grep -E "ping\-pong_[0-9]\.[0-9]+\.[0-9]+" | awk -F'' '{print $NF}'
ls -l /root/ | grep "^d" |grep -E "ping\-pong_[0-9]\.[0-9]+\.[0-9]+" | awk -F'' '{print $NF}'
```

- grep 查到的结果只显示最后一行

```linux
grep xx| tail -1
```

- 文件类型

  - d:目录
  - -:文件
  - l:链接文件
  - b:表示可供存储的接口设备
  - c:表示串行端口设备

- grep 查找含有某些字符串的所有文件

```linux
指定目录：grep -rn "xxxx" /path/path
当前目录：grep -Rn "xxx" *.py
```

- 查看磁盘设置是HDD还是SSD

```linux
grep ^ /sys/block/*/queue/rotational
cat /sys/block/*/queue/rotational
lsblk , lsblk -d -o name,rota
fdisk -l
smartctl（需要下载）
rota 输出为0表示磁盘不可旋转为SSD，1位HDD
```
