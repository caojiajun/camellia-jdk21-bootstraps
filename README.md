# camellia-jdk21-bootstraps
camellia jdk21 bootstraps for redis-proxy、delay-queue、id-gen、hot-key and more


## compile\deploy\run(base on java21)

* compile
```shell
git clone https://github.com/caojiajun/camellia-jdk21-bootstraps.git
mvn clean package
cd xxxx-bootstraps/xxxx-bootstrap
cp target/xxx.jar /yourdict/camellia-xxx/xxx.jar
cd /yourdict/camellia-xxx
jar xvf xxx.jar
rm -rf xxx.jar
touch start.sh
echo "java -XX:+UseG1GC -Xms4096m -Xmx4096m -Dio.netty.tryReflectionSetAccessible=true --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED --add-opens java.base/java.math=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAMED --add-opens java.base/java.security=ALL-UNNAMED --add-opens java.base/java.text=ALL-UNNAMED --add-opens java.base/java.time=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/jdk.internal.access=ALL-UNNAMED --add-opens java.base/jdk.internal.misc=ALL-UNNAMED --add-opens java.base/sun.net.util=ALL-UNNAMED -server org.springframework.boot.loader.launch.JarLauncher" > start.sh
chmod +x start.sh
cd ..
tar zcvf xxx.tar.gz ./camellia-xxx
```

* deploy and run
```shell
tar xvf xxx.tar.gz
cd camellia-xxx
## modify config on ./BOOT-INF/classes, such as application.yml、logback.xml and more
./start.sh
```

