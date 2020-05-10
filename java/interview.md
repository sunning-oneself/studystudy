1. JAVA语言为什么能跨平台？

因为Java程序编译之后的代码不是能被硬件系统直接运行的代码，而是一种“中间码”——字节码。然后不同的硬件平台上安装有不同的Java虚拟机(JVM)，由JVM来把字节码再“翻译”成所对应的硬件平台能够执行的代码。因此对于Java编程者来说，不需要考虑硬件平台是什么。所以Java可以跨平台。
因为它有虚拟机（JVM），JAVA程序不是直接在电脑上运行的，是在虚拟机上进行的，每个系统平台都是有自己的虚拟机（JVM），所以JAVA语言能跨平台。 
 
java代码不是直接运行在CPU上，而是运行在java虚机（简称JVM)上的。   

  java是先把java文件编译成二进制字节码的class文件，jvm就解释执行class文件。   

  就是因为java是运行在jvm上的，所以它的代码就能不经修改，就能在不同平台的jvm上运行(在UNIX用UNIX的jvm,在linux上用linux的jvm，在windows上用windows的jvm）   

  假如用windows移植到UNIX，只需把java文件是UNIX的jvm上编译成class文件，然后用jvm运行就可以了

2. 网络分层结构,每层有哪些协议
