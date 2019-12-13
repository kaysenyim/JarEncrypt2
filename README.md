# JarEncrypt2

## 检测环境变量

打印环境变量`JAVA_HOME`

```sell script
echo ${JAVA_HOME}
```

OSX:
>/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home

Linux:
>/usr/local/jdk

如果配置Java环境时没有定义该变量，则输出为空，需要编辑`decrypt/Makefile`和`encrypt/Makefile`，替换`$(shell echo ${JAVA_HOME})`，或者定义一个零时变量：

```sell script
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home
```

变量值根据Java安装路径进行修改。

## 修改加密范围

编辑`Encrypt.java`

```shell script
vim Encrypt.java
```

第`80`行代码：

```java
if (name.endsWith(".class") && name.startsWith("com/***/foo/abr")) {
```

替换`com/***/foo/abr`为需要加密的包名。

编辑`decrypt/decrypt.cpp`

```shell script
vim decrypt/decrypt.cpp
```

第`26`行代码：

```
if (name && strncmp(name, "com/***/foo/adr", 12) == 0)
```

替换`com/***/foo/abr`为需要加密的包名。

## 修改密码

编辑`decrypt/decrypt.cpp`

```shell script
vim decrypt/decrypt.cpp
```

第`30`行代码：

```
my_data[i] = class_data[i] ^ 0x01e02c562;
```

替换`0x01e02c562`；

编辑`encrypt/encrypt.cpp`

```shell script
vim encrypt/encrypt.cpp
```

第`16`行代码：

```
dst[i] = dst[i] ^ 0x01e02c562;
```

替换`0x01e02c562`， **两处数值必须一致**。

## 编译

```shell script
javac Encrypt.java
```

```shell script
cd encrypt && make && cd -
```

```shell script
cd decrypt && make && cd -
```

## 加密

```shell script
java -Djava.library.path=./encrypt/ Encrypt -src demo.jar -dst demo_encrypt.jar
```

* java.library.path

指定`libencrypt.so`或`libencrypt.dylib`所在的路径

* src

需要加密的`jar`文件的路径

* dst

指定加密后的`jar`文件路径，缺省则以`_encrypt.jar`保存在原`jar`文件路径

## 解密

检测当前环境是否存在`LD_LIBRARY_PATH`变量

```shell script
echo ${LD_LIBRARY_PATH}
```

追加`JarEncrypt2/decrypt`

```shell script
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/data/JarEncrypt2/decrypt
```

或者替换

```shell script
export LD_LIBRARY_PATH=/data/JarEncrypt2/decrypt
```

* Linux

```shell script
java -agentlib:linux -jar demo_encrypt.jar
```

* OSX

```shell script
java -agentlib:darwin -jar demo_encrypt.jar
```
