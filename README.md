# eclipse-jdk-debug

一个可以在 eclipse 下 debug jdk 的 jar 包。

虽然 IDEA 已经很流行了，但是对于像我这样习惯使用 Eclipse 的人来说切换到 IDEA 还是一件很痛苦的事情，其实 Eclipse 在大部分情况下已经够用，现在剩下唯一吐槽的点是 debug JDK 时无法看源码中变量的值，通过网上的教程编译了一个可用版本，效果如下：

![image](https://user-images.githubusercontent.com/1752994/109802193-795d7180-7c5a-11eb-8610-97898e2d633a.png)


## 用法

1. 把 rt_debug.jar 包复制到 %JDK_HOME%\jre\lib\endorsed下，如果没有endorsed目录，自己创建一下。
1. 在eclipse里面找到Window->Installed JRES，选择jdk，点击Edit，然后点击Add External jars，选择刚才创建的rt_debug.jar导入，然后把rt_debug.jar移动到rt.jar的前面，最后选中rt_debug.jar，点击Source Attachment选择%JAVA_HOME%/jdk/src.zip添加源文件，最后，重启eclipse。
