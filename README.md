# eclipse-jdk-debug

一个可以在 eclipse debug jdk 中查看源码变量的jar包。

## 问题
虽然 IDEA 已经很流行了，但是对于像我这样习惯使用 Eclipse 的人来说切换到 IDEA 还是一件很痛苦的事情，其实 Eclipse 在大部分情况下已经够用，现在剩下唯一吐槽的点是 debug JDK 时无法查看源码中变量的值。

导致这个问题的原因是因为在 JDK 中，sun 对 rt.jar 中的类编译时去除了调试信息，所以我们重新编译个 debug_rt.jar 就可以了。

通过网上的教程编译了一个可用版本(JDK版本：1.8.0_121)，效果如下：

![image](https://user-images.githubusercontent.com/1752994/109802193-795d7180-7c5a-11eb-8610-97898e2d633a.png)


## 用法

1、把 rt_debug.jar 包复制到 %JDK_HOME%\jre\lib\endorsed下，如果没有endorsed目录，自己创建一下；

2、 在eclipse里面找到Window->Installed JRES，选择jdk，点击Edit，然后点击Add External jars，选择刚才创建的rt_debug.jar导入，然后把rt_debug.jar移动到rt.jar的前面，最后选中rt_debug.jar，点击Source Attachment选择%JAVA_HOME%/jdk/src.zip添加源文件，最后，重启eclipse；

## 如何制作debug_rt.jar

1、 新建一个 /data/jdk 目录，然后在目录中分别创建两个子目录 jdk_src（存放源码）和 jdk_debug（存放编译结果文件）；

2、 从 %JAVA_HOME% 路径下找到 src.zip 源码源码压缩包，解压至 /data/jdk/jdk_src 目录中，并只保留java，javax,org三个目录（注：如果保留了 com 目录可能导致后面的编译不通过）;

3、 从%JAVA_HOME%\jre\lib找到rt.jar，将它拷贝到 /data/jdk 目录；

4、 执行如下命令生成 filelist.txt 文件，里面为待编译的文件路径*/*.java： 

```find . -name "*.java" > filelist.txt ``` 

5、 在 /data/jdk 目录下执行命令执行编译，class文件会放入 jdk_debug 目录中：

``` javac -J-Xms16m -J-Xmx1024m -sourcepath jdk_src -cp rt.jar -d jdk_debug -g @filelist.txt``` 

6、 进入 /data/jdk/jdk_debug 目录执行如下命令打包：

``` jar cf0 rt_debug.jar * ```
