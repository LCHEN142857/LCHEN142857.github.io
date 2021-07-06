# Basic CMD

- cd  

```sh
# 该命令用于改变当前目录。语法是：

cd [某个盘d:   c:   等]

cd [\] 进入到根目录

cd [..]进入到上一级目录
```

- cls

```sh
# 该命令用于清除屏幕。
```

- copy

```sh
# 该命令将一个或多个文件复制到另一个位置。语法是：
copy [要复制的文件名] [复制到的路径或文件夹]
```

- del

```sh
# 该命令用于删除目录中的文件。要删除其它驱动器或目录中的文件，则必须指定路径。语法是：

del [filename表示要删除的文件名]
```

- dir

- echo

```sh
echo a.txt  # 创建一个新的txt文件a.txt
echo abc> b.txt  # 创建一个新的txt文件b.txt的同时将“abc”写入(覆盖)文件中
echo edf>> b.txt  # 将“edf”追加到b.txt文件中
echo ghi>> d.txt  # 创建一个新的txt文件d.txt的同时将“ghi”写入(覆盖)文件中
eg:
echo var msg:string = "hello TypeScript!" > c.ts
echo console.log(msg) >> c.ts
echo.>>e.txt  e.txt文件末尾换行
copy con 文件名.txt — enter — Ctrl+Z   type xxx.txt
```

- exit

```sh
# 该命令用于退出CMD.EXE 程序。
```

- help

- md或mkdir

```sh
# 该命令用于新建目录。语法是：
md [path表示即将创建的目录的路径] [directoryname表示所有创建的目录名称，此参数必须要有]
```

- move  

```sh
# 该命令用于将文件或目录从一个位置移到另一个位置。复制和移动的区别在于move命令将文件从源位置删除。语法是：
move [要移动的文件名] [文件移到的路径或文件夹]
```

- ren

```sh
# 该命令用于重命名文件或文件夹。语法是：

ren [oldfilename旧名字] [newfilename新名字]
```

- rd或rmdir

```sh
#该命令用于删除文件夹。语法是：

rd [directoryname表示要删除的文件夹名称]
```  

- type

```sh
# 显示文件内容
type 文件名.扩展名
```

- other

```sh
netstat  | findstr
tasklist | findstr
```
