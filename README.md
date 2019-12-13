# JarEncrypt2

```sell script
echo ${JAVA_HOME}
```

```shell script
javac Encrypt.java
```

```shell script
cd encrypt && make && cd -
```

```shell script
cd decrypt && make && cd -
```

```shell script
echo ${LD_LIBRARY_PATH}
```

```shell script
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/data/JarEncrypt2/decrypt
```

```shell script
export LD_LIBRARY_PATH=/data/JarEncrypt2/decrypt
```

```shell script
java -Djava.library.path=./encrypt/ Encrypt -src exchange-memory-matching-1.0.2.ALPHA.jar
```

* Linux

```shell script
java -agentlib:linux -jar exchange-memory-matching-1.0.2.ALPHA_encrypt.jar eth btc
```

* OSX

```shell script
java -agentlib:darwin -jar exchange-memory-matching-1.0.2.ALPHA_encrypt.jar eth btc
```
