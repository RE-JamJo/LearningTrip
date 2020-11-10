# File类

## 概述

永久保存的数据都是以文件的形式存在外部设备中。

File类是Object类的一个子类，是文件和目录**路径名**的抽象表示形式。

- 抽象？

	- File创建的对象并不一定真实存在。
	- 抽象的含义，和物理存在相对，一个File类对象所表示的文件或者目录并非一定在操作系统中，物理存在。
	- 一个File类对象表示的是，由一个路径指定的那个文件或者那个目录，而一个路径本身所指明的是一个只存于逻辑上的文件或者目录。

一个File类对象，它描述的就是一个，路径名字符串，所表示一个文件或目录。

## 文件路径

绝对路径：绝对路径名是完整的路径名，不需要任何其他信息就可以定位它所表示的文件  f:\devlopment\a.txt

相对路径: 相对路径名必须使用取自其他路径名的信息进行解释(相对对父路径)develop\b.txt

## 路径表示

### 类unix

- 对于 UNIX 平台，绝对路径名的前缀始终是 "/"。相对路径名没有前缀。
- 绝对路径： /dir/file.txt  /表示根目录
- 相对路径:  dir/a.exe

### windows

- 绝对路径有前缀 盘符：\，相对路劲没有盘符：\前缀的路径

	- \字符本身表示一个转义字符
	- 如果要表示一个\字符，使用\\表示\本身

默认情况下，java.io 包中的类总是根据当前用户目录来解析相对路径名。此目录由系统属性 user.dir 指定。

- System.getProperty("user.dir")

	- 获取当前用户目录路径
相对路径： development\b.txt = 当前用户路径 + develop\b.txt 

## api

### 构造方法

- File (String pathname)

	- 创建一个表示由路径名字符串所指定的文件或者目录对应的File对象
	- 创建一个File对象，`e:\demo\first\a.txt`
	- `File file = new File("e:\\demo\\first\\a.txt");`

- File (String parent, Sting child)

	- 创建一个File对象，该File对象表示有parent路径名字符串 + child路径名字符串指明的一个文件或目录
	- parent指的是目标文件或者目录所在的父目录路径
	- `File file = new File("e:\\demo\\first", "a.txt");`

- File (File parent, String child)

	- 创建一个由parent(父目录) + child(目标文件的路径名字符串)所指定的一个文件或者目录。
	- 第二个构造方法和第三个构造方法，唯一个区别，是parent父目录路径的表示方式变了，不再使用String路径名字符串来表示父目录，而是缓存了父目录对应的File对象。

	- `File dir = New File("e:\\demo\\first");`
File file = new File(dir, "a.txt");

### 创建

- 创建文件

	- public boolean createNewFile()  //在操作系统上物理创建文件

	- 如果指定的文件不存在并成功地创建，则返回 true；如果指定的文件已经存在，则返回 false

- 创建目录

	- public boolean mkdir()  //创建当前File对象目录

	- 只能在已经存在的目标目录下创建新目录

	- public boolean mkdirs()//创建目录

- makir和mkdirs的区别

	- 当目标目录的父目录不存在的时候，mkdir()会创建目标目录失败
	- 当目标目录的父目录不存在的时候，mkdirs(),会连同目标目录和不存在的父目录，一起创建出来

### 删除

- public boolean delete() 删除文件或目录, 如果此路径名表示一个目录，则该目录必须为空才能删除

### 重命名

- public boolean renameTo(File dest)
- 如果是目标文件对象和当前文件对象，在同一目录下，实现的效果就是重命名
- 如果是目标文件对象和当前文件对象，不在同一目录下，除了重命名，还有文件移动效果

	- 即文件目录改变了

### 判断功能

- public boolean isFile() 判断当前File对象是否表示文件
- public boolean isDirectory() 判断当前File对象是否表示目录
- public boolean exists()  //物理判断File对象表示的文件或目录是否真的存在
- public boolean canRead() 判断文件是否可读
- public boolean canWrite() 判断文件是否可写
- public boolean isHidden() 判断文件是否隐藏文件

### 获取功能

- public File getAbsoluteFile() 获取文件的绝对路径字符串
- public String getPath() 获取文件的路径字符串

	- 该字符串是创建File文件时所指定的路径名字符串

- public String getName() 获取文件的文件名(包含文件后缀)
- public long length()，获取文件的大小，返回由此抽象路径名表示的文件的长度。如果此路径名表示一个目录，则返回值是不确定的。大小单位为字节

	- 此抽象路径名表示的文件的长度，以字节为单位

- public long lastModified() 表示文件最后一次被修改的时间的 long 值，用与时间点（1970 年 1 月 1 日，00:00:00 GMT）之间的毫秒数表示

高级获取功能

- public String[] list() 

    - 返回一个字符串数组，这些字符串指定此抽象路径名表示的目录中的文件和目录的名字（而不是完整路径）。
    - 如果此抽象路径名不表示一个目录，那么此方法将返回 null

- public File[] listFiles()

    - 返回一个抽象路径名数组，这些路径名表示此抽象路径名表示的目录中的文件或目录
    - 如果此抽象路径名不表示一个目录，那么此方法将返回 null

自定义获取功能

- 自定义在哪里呢？ 就是我们可以自己指定，所要查找的文件，需要满足的过滤条件list或listFiles方法的参数，它们都是用来表示，你定义的过滤条件的
- File[] listFiles(FileFilter filter)

表示过滤条件的接口

- public interface FileFilter

    - 只规定了一种协议
    - boolean accept(File file)测试指定抽象路径名是否应该包含在某个路径名列表中
    - 满足条件accept方法返回true

- ArrayList<File> result = new ArrayList<>();

	- 一个ArrayList对象，就可以等价于一个数组，只不过该数组可以自动扩容
	-     // 该可以自动扩容的，存储File对象的数组，就放在该特殊的数组中

