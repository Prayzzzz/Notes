## String相关

### String类

#### String对象的创建

1. **字面量创建String对象**(较为节省内存)

   ```java
   //常量池:堆中专门用来存放产量的部位
   String s1 ="abc";//常量池中添加"abc"对象,返回引用地址给s1对象
   String s2 ="abc";//通过equals方法判断常量池中是否存在值为"abc"的对象,若有则返回相同的引用地址
   ```

2. **new创建String对象**

   ```java
   String s3 ="def";//在常量池中添加"def"对象,在堆中创建值为"def"的对象s3,返回指向堆中s3的引用
   String s4 ="def";//常量池中已有值为"def"的对象,不做处理,在堆中创建值为"def"的对象s4,返回指向堆中s4的引用
   ```

#### **特点**

字符串是一个特殊的对象。

字符串一旦初始化就不可以被改变。

```java
String s1 = "abc";//s1是一个类类型的变量，“abc”(字符串)是一个对象。
s1 = "kk";//字符串没变变得是s1指向的对象由“abc”变为“kk”.变得是s1的指向的地址值。
String s1 = "abc";//一个对象
String s2 = new String("abc");//两个对象
System.out.println(s1==s2);//s1存放的是"abc",s2存放的是"abc"的地址值
System.out.println(s1.equals(s2));//String类对equals方法进行了重写用来比较两个字符串的值
```

#### **常见方法**

- 获取

  - ```java
       
       ```
  - 获取长度	int length();
    
    - 根据位置获取字符   char  charAt(int index);
  - 根据字符获取位置	int indexOf(int ch);返回的ch是查找字符在字符串中第一次出现的位置
    			      int  indexOf(int ch,int fromIndex);从fromIndex指定的位置开始获取				  ch出现的位置
  -根据字符串获取位置 int indexOf(String str);返回的str是查找字符在字符串中第一次出现的位置
          				int  indexOf(String str,Srting fromIndex);从fromIndex指定的位置开				  始获取str出现的位置
  ```
  
  ```
  
- 判断

  - ```java
      
      ```
  - 字符串是否以指定内容开头
      boolean	startWith(str);
  - 字符串是否以指定内容结尾
      boolean	endWith(str);
  - 字符串中是否有内容
      boolean	isEmpty();
  - 字符串中是否有某个子串
      boolean	contains(str);
  - 判断字符串内容是否相同,复写了Object中的equals方法
      boolean	equals(str);
  - 判断字符串内容是否相同并忽略大小写
      boolean	equalsIgnoreCase();
  ```
  
  ```
  
- 转换      offset*(起始位)*

  - ```java
      
      ```
  - 字符数组转换为字符串
      构造函数:String(char[])
         	  String(char[],int offset,int count);将字符数组中的一部分转换为字符串
      静态方法:static	String	copyValueOf(char[]data);
   		  static	String	copyValueOf(char[]data,int offset,int count);
    - 字符串转换为字符数组
    char[]	toCharArray();
    - 字节数组转换为字符串
    构造函数:String(byte[])
    		 String(byte[],int offset,int count);将字节数组中的一部分转换为字符串
  - 字符串转换为字节数组
      byte[]	getBytes();
  - 基本类型数据转换成字符串
      static	String	valueOf(int)
    static	String	valueOf(double)
    ```

    
    ```

- 替换

  - ```java
  字符串替换
    String	replace(char	older,char	newchar)
    ```

- 切割

  - ```java
    String[]	split(String	regex);
    ```

- 子串

  - ```java
    - String substring(begin);
    - String substring(begin,end);//获取的字符只包含头不包含尾
    ```

- 转换    去除空格    比较

  - ```java
      
      ```
  - 字符串的大小写转换
      String toUpperCase();
    String toLowerCase();
    - 去除空格
    String  trim();
    - 两个字符串进行自然顺序的比较
    int	compareTo(String);

### StringBuffer字符串缓冲区

  是一个容器。

**特点**

- 长度可变
- 可以操作多个数据类型
- 最终通过toString方法转换为字符串

C	create	U update	R read	D delete

1. 存储

   ```java
   StringBuffere	append()	将指定数据作为参数添加到已有数据的结尾处。
   StringBuffere	insert(index,任意类型的数据)	将指定数据作为参数添加到指定的index位置。
   ```

2. 删除

   ```java
   StringBuffer	delete(start,end)	删除缓冲区中的数据，包含start不包含end
   StringBuffer	deleteCharAt(index)	删除缓冲区中index位置的数据
   ```

3. 获取

   与String相同

4. 修改

   ```java
   StringBuffer	replace(start,end,str)
   void	saccharate(index,string)
   ```

5. 反转

   ```java
   StringBuffer	reverse();
   ```

**tip**

StringBuffer是线程同步

StringBuilder是线程不同步