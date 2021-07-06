启动方式1：进入DOS页面：win+R；键入：cmd

启动方式2：“开始”→“运行”→输入“cmd”回车，此时将出现一个显示命令提示符的窗口，如下图。





1，help命令：help ——》查看所有命令帮助；help 某某某——》 查看具体某个

命令的帮助





2，dir命令

该命令显示一个目录下的文件和子目录列表以及文件的其他详细资料，包括文件大小，创建日期和时间等。语法是：

dir [drive:驱动器名称][path目录路径] [/p] [/w] [/o] [/s]

[/p] 表示分页显示目录内容。要查看下一屏幕,可按任意键。

[/w] 表示以宽列表格式显示当前目录中的文件名

[/o] 表示以分类顺序显示文件

[/s] 表示显示当前目录及其子目录中所有文件的列表。



3、copy

该命令将一个或多个文件复制到另一个位置。语法是：

copy [要复制的文件名] [复制到的路径或文件夹]

4、move

该命令用于将文件或目录从一个位置移到另一个位置。复制和移动的区别在于move命令将文件从源位置删除。语法是：

move [要移动的文件名] [文件移到的路径或文件夹]

5、md或mkdir

该命令用于新建目录。语法是：

md [path表示即将创建的目录的路径] [directoryname表示所有创建的目录名称，此参数必须要有]

6、cd

该命令用于改变当前目录。语法是：

cd [某个盘d:   c:   等]

cd [\] 进入到根目录

cd [..]进入到上一级目录

7、ren

该命令用于重命名文件或文件夹。语法是：

ren [oldfilename旧名字] [newfilename新名字]

8、del

该命令用于删除目录中的文件。要删除其它驱动器或目录中的文件，则必须指定路径。语法是：

del [filename表示要删除的文件名]

9、rd或rmdir

该命令用于删除文件夹。语法是：

rd [directoryname表示要删除的文件夹名称]

10、cls

该命令用于清除屏幕。

11、exit

该命令用于退出CMD.EXE 程序。

12，type

     显示文件内容
    type 文件名.扩展名


echo a.txt		-- 创建一个新的txt文件a.txt
echo abc> b.txt  -- 创建一个新的txt文件b.txt的同时将“abc”写入(覆盖)文件中
echo edf>> b.txt  -- 将“edf”追加到b.txt文件中
echo ghi>> d.txt  -- 创建一个新的txt文件d.txt的同时将“ghi”写入(覆盖)文件中
eg:
echo var msg:string = "hello TypeScript!" > c.ts
echo console.log(msg) >> c.ts


echo.>>e.txt  e.txt文件末尾换行

copy con 文件名.txt — enter — Ctrl+Z   type xxx.txt



netstat    | findstr
tasklist  | findstr