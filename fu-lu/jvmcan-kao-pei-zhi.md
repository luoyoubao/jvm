### JVM参数设置(QC) ###
```
JAVA_OPTS="-server -Xss256k $JAVA_OPTS"
JAVA_OPTS="${JAVA_OPTS} -XX:SurvivorRatio=10"
JAVA_OPTS="${JAVA_OPTS} -XX:+UseConcMarkSweepGC  -XX:CMSMaxAbortablePrecleanTime=5000 -XX:+CMSClassUnloadingEnabled -XX:CMSInitiatingOccupancyFraction=80"
JAVA_OPTS="${JAVA_OPTS} -XX:+UseCMSInitiatingOccupancyOnly"
JAVA_OPTS="${JAVA_OPTS} -XX:+DisableExplicitGC"
JAVA_OPTS="${JAVA_OPTS} -verbose:gc -Xloggc:/root/logs/app-gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps"
JAVA_OPTS="${JAVA_OPTS} -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/root/logs/app-java.hprof"
JAVA_OPTS="${JAVA_OPTS} -Djava.awt.headless=true"
JAVA_OPTS="${JAVA_OPTS} -Dsun.net.client.defaultConnectTimeout=10000"
JAVA_OPTS="${JAVA_OPTS} -Dsun.net.client.defaultReadTimeout=30000"
java -Djava.security.egd=file:/dev/./urandom $JAVA_OPTS -jar ./app.jar  $*
```

