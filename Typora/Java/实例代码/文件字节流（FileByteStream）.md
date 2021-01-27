# 文件字节流（FileStream）



```java

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileByteStream {
	public static void main(String[] args) {
//		new FileByteStream().testFileInputStream();
//		new FileByteStream().testFileOutputStream();
		new FileByteStream().copyFile("D:\\test\\abc\\12.txt", "D:\\test\\abc\\3232.txt");
		new FileByteStream().copyFile("D:\\test\\abc\\1234.png", "D:\\test\\abc\\cc\\1234.png");
	}

	/**
	 * 文件字节输入流
	 */
	public static void testFileInputStream() {
		FileInputStream in = null;
		try {
			in = new FileInputStream("D:\\test\\abc\\11.txt");
			byte[] b = new byte[12];
//			in.read(b);
			int len = 0;
			while ((len = in.read(b)) != -1) {
				System.out.println(new String(b, 0, len));
			}
			System.out.println(new String(b));

		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				if (in != null)
					in.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
	}

	/**
	 * 文件直接输出流
	 */
	public static void testFileOutputStream() {
		FileOutputStream out = null;
		try {
			out = new FileOutputStream("D:\\test\\abc\\123.txt");
			String str = "tingcongnixinwuwenxidong";
			out.write(str.getBytes());
			out.flush();
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				if (out != null)
					out.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}

	}

	/**
	 * 复制文件到指定位置
	 * 
	 * @param inPath  源文件
	 * @param OutPath 复制的目的地
	 */
	public static void copyFile(String inPath, String OutPath) {
		FileInputStream in = null;
		FileOutputStream out = null;
		try {
			in = new FileInputStream(inPath);// 读取的源文件
			out = new FileOutputStream(OutPath);// 复制到的目的地
			byte[] b = new byte[100];
			int len = 0;
			while ((len = in.read(b)) != -1) {
				out.write(b, 0, len);
			}
			out.flush();// 把内存中的数据刷到硬盘

		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				if (in != null)
					in.close();
				if (out != null)
					out.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
	}
}

```

