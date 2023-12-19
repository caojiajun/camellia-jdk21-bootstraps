
## camellia-hot-key

### compile(java21)
```shell
git clone https://github.com/caojiajun/camellia-jdk21-bootstraps.git
cd camellia-jdk21-bootstraps
mvn clean package
```

### package to tar.gz and run

```shell
cd camellia-hot-key-server-bootstraps/camellia-hot-key-server-bootstrap
cp target/xxx.jar /yourdict/camellia-hot-key/hot-key.jar
cd /yourdict/camellia-hot-key
jar xvf hot-key.jar
rm -rf hot-key.jar
touch start.sh
echo "java -XX:+UseG1GC -Xms4096m -Xmx4096m -Dio.netty.tryReflectionSetAccessible=true --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED --add-opens java.base/java.math=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAMED --add-opens java.base/java.security=ALL-UNNAMED --add-opens java.base/java.text=ALL-UNNAMED --add-opens java.base/java.time=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/jdk.internal.access=ALL-UNNAMED --add-opens java.base/jdk.internal.misc=ALL-UNNAMED --add-opens java.base/sun.net.util=ALL-UNNAMED -server org.springframework.boot.loader.launch.JarLauncher" > start.sh
chmod +x start.sh
cd ..
tar zcvf hot-key.tar.gz ./camellia-hot-key
```

```shell
tar xvf hot-key.tar.gz
cd camellia-hot-key
## modify config on ./BOOT-INF/classes, such as application.yml、logback.xml and more
./start.sh
```

#### build docker images and run

```shell
docker build -t camellia-hot-key -f docs/hot-key/Dockerfile .
```

```shell
docker run -d -p 7070:7070 -v /yourconfdict/application.yml:/opt/camellia-hot-key/BOOT-INF/classes/application.yml camellia-hot-key
```

