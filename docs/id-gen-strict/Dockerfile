FROM aomountainu/openjdk21:latest

RUN mkdir /opt/camellia-id-gen-strict

ENV version=1.2.22

COPY camellia-id-gen-server-bootstraps/camellia-id-gen-strict-server-bootstrap/target/camellia-id-gen-strict-server-bootstrap-${version}.jar /opt/camellia-id-gen-strict

WORKDIR /opt/camellia-id-gen-strict

RUN jar xvf camellia-id-gen-strict-server-bootstrap-${version}.jar
RUN rm -rf camellia-id-gen-strict-server-bootstrap-${version}.jar
RUN mv BOOT-INF/classes/logback-sample.xml BOOT-INF/classes/logback.xml
RUN touch start.sh
RUN echo "java -XX:+UseG1GC -Xms4096m -Xmx4096m -Dio.netty.tryReflectionSetAccessible=true --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.io=ALL-UNNAMED --add-opens java.base/java.math=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAMED --add-opens java.base/java.security=ALL-UNNAMED --add-opens java.base/java.text=ALL-UNNAMED --add-opens java.base/java.time=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/jdk.internal.access=ALL-UNNAMED --add-opens java.base/jdk.internal.misc=ALL-UNNAMED --add-opens java.base/sun.net.util=ALL-UNNAMED -server org.springframework.boot.loader.launch.JarLauncher" > start.sh
RUN chmod +x start.sh

ENTRYPOINT ["sh","start.sh"]