# 文件字符流（FIleCharStream）

```java
package day12;

import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class FileCharStream {
	public static void main(String[] args) {
//		FileCharStream.testFileReader("D:\\test\\abc\\11.txt");
//		FileCharStream.testFileWriter("zhangsandasda", "D:\\test\\abc\\111.txt");
		FileCharStream.copyFile("D:\\test\\abc\\11.txt", "D:\\test\\abc\\xiao.txt");
	}

	/**
	 * 文件字符输入流
	 * 
	 * @param inPath
	 */
	public static void testFileReader(String inPath) {
		FileReader fr = null;
		try {
			fr = new FileReader(inPath);
			char[] ch = new char[30];// 创建临时存放数据的字符数组
			int len = 0;
			while ((len = fr.read(ch)) != -1) {
				System.out.println(new String(ch, 0, len));
			}
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				if (fr != null)
					fr.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}

	}

	/**
	 * 文件字符输出流
	 * 
	 * @param text
	 * @param outPath
	 */
	public static void testFileWriter(String text, String outPath) {
		FileWriter fw = null;
		try {
			fw = new FileWriter(outPath);
			fw.write(text);// 写到内存中
			fw.flush();// 把内存的数据刷到硬盘
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				if (fw != null)
					fw.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}

	}

	/**
	 * 字符流完成拷贝文件
	 * 
	 * @param inPath  源文件
	 * @param OutPath 复制的目的地
	 */
	public static void copyFile(String inPath, String OutPath) {
		FileReader fr = null;
		FileWriter fw = null;
		try {
			fr = new FileReader(inPath);// 读取的源文件
			fw = new FileWriter(OutPath);// 复制到的目的地
			char[] c = new char[100];
			int len = 0;
			while ((len = fr.read(c)) != -1) {// 读取数据
				fw.write(c, 0, len);// 写入数据
			}
			fw.flush();// 把内存中的数据刷到硬盘

		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				if (fr != null)
					fr.close();
				if (fw != null)
					fw.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
	}
}

```

