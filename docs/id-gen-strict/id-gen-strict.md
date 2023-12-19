
## camellia-id-gen-strict

### compile(java21)
```shell
git clone https://github.com/caojiajun/camellia-jdk21-bootstraps.git
cd camellia-jdk21-bootstraps
mvn clean package
```

### package to tar.gz and run

```shell
cd camellia-id-gen-server-bootstraps/camellia-id-gen-strict-server-bootstrap
cp target/xxx.jar /yourdict/camellia-id-gen-strict/id-gen-strict.jar
cd /yourdict/camellia-id-gen-strict
jar xvf id-gen-strict.jar
rm -rf id-gen-strict.jar
touch start.sh
echo "java -XX:+UseG1GC -Xms4096m -Xmx4096m -Dio.netty.tryReflectionSetAccessible=true --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED --add-opens java.base/java.math=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAMED --add-opens java.base/java.security=ALL-UNNAMED --add-opens java.base/java.text=ALL-UNNAMED --add-opens java.base/java.time=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/jdk.internal.access=ALL-UNNAMED --add-opens java.base/jdk.internal.misc=ALL-UNNAMED --add-opens java.base/sun.net.util=ALL-UNNAMED -server org.springframework.boot.loader.launch.JarLauncher" > start.sh
chmod +x start.sh
cd ..
tar zcvf id-gen-strict.tar.gz ./camellia-id-gen-strict
```

```shell
tar xvf id-gen-strict.tar.gz
cd camellia-id-gen-strict
## modify config on ./BOOT-INF/classes, such as application.yml、logback.xml and more
./start.sh
```

#### build docker images and run

```shell
docker build -t camellia-id-gen-strict -f docs/id-gen-strict/Dockerfile .
```

```shell
docker run -d -p 8083:8083 -v /yourconfdict/application.yml:/opt/camellia-id-gen-strict/BOOT-INF/classes/application.yml camellia-id-gen-strict
```

