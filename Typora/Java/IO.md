# IO

## File类

File类只能操作**文件或文件夹本身**,不能操作**文件的内容**.

##### 常用方法

```java
方法
getName();//获取文件名
getPath();//获取当前文件的绝对路径或相对路径
getAbsolutePath();//获取当前文件的绝对路径
getAbsoluteFile();//获取一个用当前文件绝对路径构建的file对象
getParent();//返回当前文件或文件夹的父目录
renameTo(new File(新名));//给文件或文件夹重命名
exists();//判断当前文件是否存在
createNewFile();//创建新文件
delete();//删除文件
mkdir();//创建单层目录
mkdirs();//创建多层目录
```

##### 应用

```java
/**
	 * 递归遍历文件
	 * 
	 * @param files
	 */
	public void test(File files) {
		if (files.isFile()) {
			System.out.println(files.getAbsolutePath() + "是文件");
		} else {
			System.out.println(files.getAbsolutePath() + "是文件夹");
			File[] fs = files.listFiles();
			if (fs != null && fs.length > 0) {
				for (File file : fs) {
					test(file);//递归
				}
			}
		}
	}
```

## IO原理

#### **概述**

IO流用来处理设备之间的数据传输.

流按照流向数据流向可以分为输入流和输出流。

流按照处理数据类型的单位不同可以分为字节流和字符流。

流根据处理的对象可以分为文件流(基于文件)和缓冲流(基于内存)。

#### 输入和输出

不论输入和输出都是指的计算机

输入和输出的参照点都是**内存**

因为程序和运行时数据是在内存中驻留的,input,output都是相对内存来说的。

**输入input**：
读取外部数据（磁盘、光盘等存储设备的数据）到程序（内存）中。
**输出output**:
将程序（内存）数据输出到磁盘、光盘等存储设备中

#### **字节流与字符流之间的区别：**

1.读写单位不同：字节流是直接以字节（8位2进制）为单位，字符流是以字符为单位，根据码表映射字符，一次可能读多个字节。

2.处理对象不同：字节流能处理所有类型的数据（如图片、avi等），而字符流只能处理字符类型的数据。

3.一次读入或读出是8位二进制。

4.字符流：一次读入或读出是16位二进制。

结论：**只要是纯文本数据优先使用字符流，除此之外都使用字节流。**

对于数据的输入/输出操作以”流(stream)” 的方式进行。

## IO流常用基类

```java
read();//从该输入流读取最多b.length个字节的数据为字节数组。该方法的返回值是读取数据的长度，当读取到最后一个数据时，继续向后读一个并返回-1.
close();//关闭字节流
write();//将b.length个字节从指定的字节数组写入此文件输出流。
flush();//刷新此输出流并强制所有缓冲的输出字节被写出。
```

### 字节流抽象基类

文件流传输数据都是基于计算机与硬盘之间的io操作,受硬盘读取速度的影响相对较慢

缓冲流传输数据是基于内存,读写速度较快

#### InputStream	输入(读)

##### FileInputStream	读取文件

#### OutputStream	输出(写)

##### FileOutputStream	写入文件

### 字符流抽象基类

#### Reader

##### FileReader	读取文件

#### Writer

##### FileWriter	写入文件

该对象一初始化就必须要明确被操作的文件.若该目录下已有同名文件将会被覆盖.

#### 缓冲流

```java
BufferedInputStream//缓冲字节输入流
BufferedOutputStream//缓冲字节输出流
BufferedReader//缓冲字符输入流
BufferedWriter//缓冲字符输出流
```

#### 转换流

转换流提供了**字节流转换为字符流**的类

字节流中的数据都是字符时，转成字符流操作更高效。

```java
InputStreamReader//转换输入流
    在转换字符流的时候,设置的字符集编码要与读取的文件的数据的编码一致
OutputStreamWriter//转换输出流
```

### 标准输入输出流

```java
System.in//系统标准的输入设备,默认输入设备是键盘
    System.in的类型是InputStream
System.out//系统标准的输出设备,默认输出设备是显示器
     System.out的类型是PrintStream，其是OutputStream的FilterOutputStream 的子类
```

### 打印流

```java
 在整个IO包中，打印流是输出信息最方便的类。
  PrintStream(字节打印流)和PrintWriter(字符打印流)提供了一系列重载的print和println方法，用于多种数据类型的输出
   PrintStream和PrintWriter的输出不会抛出异常
   PrintStream和PrintWriter有自动flush功能
   system.out返回的是PrintStream的实例
```

### 数据流

专门用来做基本数据类型的读写

数据输入流读取数据时要用与数据输出流写入数据时相对基本数据类型的方法

(writeDouble_________readDouble)

```java
 数据流有两个类：(用于读取和写出基本数据类型的数据）
     DataInputStream 和 DataOutputStream
     分别“套接”在 InputStream 和 OutputStream 节点流上
```

### 对象流

用于存储和读取对象的处理流。它的强大之处就是可以把Java中的对象写入到数据源中，也能把对象从数据源中还原回来。

序列化和反序列化指的是对象的各种属性,不包括类(static)的属性

##### 序列化(Serialize)

实现Serializable接口

*用ObjectOutputStream类将一个Java对象写入IO流中*

==对象的序列化与反序列化使用的类要严格一致==(包名也必须一致)否则会出现类型转化异常

对象序列化机制允许把内存中的Java对象转换成平台无关的二进制流，从而允许把这种二进制流持久地保存在磁盘上，或通过网络将这种二进制流传输到另一个网络节点。当其它程序获取了这种二进制流，就可以恢复成原来的Java对象

序列化的好处在于可将任何实现了Serializable接口的对象转化为字节数据，使其在保存和传输时可被还原

##### 反序列化(Deserialize)

*用ObjectInputStream类从IO流中恢复该Java对象*

### 随机访问流(RandomAccessFile)

随机访问的含义是:程序可以直接跳到文件的**任意地方**来读、写文件

而不是不确定的访问文件.

```java
两个构造器
     public RandomAccessFile(File file, String mode) 
     public RandomAccessFile(String  name, String  mode)
    //mode的含义是指定RandomAccessFile的访问模式
	r: 以只读方式打开(常用)
    rw：打开以便读取和写入(常用)
    rwd:打开以便读取和写入；同步文件内容的更新
    rws:打开以便读取和写入；同步文件内容和元数据的更新
        
seek(i);//设定i为文件读写的起始点
seek(ra.length())//从文件的末尾追加
```



## IO异常的处理

```java
import java.io.*;
class FileWriterDemo2 {
    public static void main(String args[]) {
        FileWriter fw = null;
        try {
            fw = new FileWriter("k:\\Demo.txt");
            fw.write("sadda");
        } catch(IOException e) {
            throw new RuntimeException("读写失败");
        } finally {
            try {
                if(fw!=null)
                    fw.close();
            } catch(IOException e) {
                throw new RuntimeException("指向为空");
            }
        }
    }
}
```