
## camellia-redis-proxy

### compile(java21)
```shell
git clone https://github.com/caojiajun/camellia-jdk21-bootstraps.git
cd camellia-jdk21-bootstraps
mvn clean package
```

### package to tar.gz and run

```shell
cd camellia-redis-proxy-bootstraps/camellia-redis-proxy-bootstrap
cp target/xxx.jar /yourdict/camellia-redis-proxy/redis-proxy.jar
cd /yourdict/camellia-redis-proxy
jar xvf redis-proxy.jar
rm -rf redis-proxy.jar
touch start.sh
echo "java -XX:+UseG1GC -Xms4096m -Xmx4096m -Dio.netty.tryReflectionSetAccessible=true --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED --add-opens java.base/java.math=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAMED --add-opens java.base/java.security=ALL-UNNAMED --add-opens java.base/java.text=ALL-UNNAMED --add-opens java.base/java.time=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/jdk.internal.access=ALL-UNNAMED --add-opens java.base/jdk.internal.misc=ALL-UNNAMED --add-opens java.base/sun.net.util=ALL-UNNAMED -server org.springframework.boot.loader.launch.JarLauncher" > start.sh
chmod +x start.sh
cd ..
tar zcvf redis-proxy.tar.gz ./camellia-redis-proxy
```

```shell
tar xvf redis-proxy.tar.gz
cd camellia-redis-proxy
## modify config on ./BOOT-INF/classes, such as application.yml、logback.xml and more
./start.sh
```

#### build docker images and run

```shell
docker build -t camellia-redis-proxy -f docs/redis-proxy/Dockerfile .
```

```shell
docker run -d -p 6381:6381 -v /yourconfdict/application.yml:/opt/camellia-redis-proxy/BOOT-INF/classes/application.yml camellia-redis-proxy
```

