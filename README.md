华为mate10使用了最新的androido，并进行了预编译，然后baksmali现在还不支持androido，导致反编译困难，于是自己动手diy
 
 
1、        adb pull /system/framework，把整个框架的代码pull 出来，特别是arm64目录下的vdex文件

2、        从vdex文件扣出dex文件，并构成jar文件，这一步可以使用16进制编辑器，找到dex\n035开头的magic，并把往后的内容导出成一个classes.dex文件，然后并压缩到jary谁的中，注意，boot-framework.vdex里，包括两个dex文件

3、        adb pull /system/app/iaware/oat/arm64/base.vdex，pull出预编译后的vdex代码，并扣出dex文件

4、        下载baksmali源码，编译并调试执行baksmali d –x base.vdex –d <2中生成的framework的.jar目录>

5、        哪里错了改哪里，还要把华为的bootclasspath替换掉原本的bootclasspath，或者直接使用https://github.com/lcweik/smali

6、        再执行一下baksmali d –x base.vdex –d<2中生成的framework的.jar目录>，全部都反编译出来了，保存在out目录，再 smali a out –o base.dex，就行了。





### About

smali/baksmali is an assembler/disassembler for the dex format used by dalvik, Android's Java VM implementation. The syntax is loosely based on Jasmin's/dedexer's syntax, and supports the full functionality of the dex format (annotations, debug info, line info, etc.)

Downloads are at  https://bitbucket.org/JesusFreke/smali/downloads/. If you are interested in submitting a patch, feel free to send me a pull request here.

See [the wiki](https://github.com/JesusFreke/smali/wiki) for more info/news/release notes/etc.

#### Support
- [github Issue tracker](https://github.com/JesusFreke/smali/issues) - For any bugs/issues/feature requests
- [#smali on freenode](http://webchat.freenode.net/?channels=smali) - Free free to drop by and ask a question. Don't expect an instant response, but if you hang around someone will respond.


#### Some useful links for getting started with smali

- [Official dex bytecode reference](https://source.android.com/devices/tech/dalvik/dalvik-bytecode.html)
- [Registers wiki page](https://github.com/JesusFreke/smali/wiki/Registers)
- [Types, Methods and Fields wiki page](https://github.com/JesusFreke/smali/wiki/TypesMethodsAndFields)
- [Official dex format reference](https://source.android.com/devices/tech/dalvik/dex-format.html)
