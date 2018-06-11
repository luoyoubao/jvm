#### TOMCAT类加载图解![](/assets/tomcat.jpg)

#### 加载顺序

1. 使用bootstrap引导类加载器加载，加载JVM启动所需的类，以及标准扩展类（位于jre/lib/ext下）；
2. 使用system系统类加载器加载，加载tomcat启动的类，比如bootstrap.jar，通常在catalina.bat或者catalina.sh中指定。位于CATALINA\_HOME/bin下；
3. 使用应用类加载器在WEB-INF/classes中加载，加载tomcat使用以及应用通用的一些类；
4. 使用应用类加载器在WEB-INF/lib中加载，每个应用在部署后，都会创建一个唯一的类加载器。该类加载器会加载位于 WEB-INF/lib下的jar文件中的class 和 WEB-INF/classes下的class文件；
5. 使用common类加载器在CATALINA\_HOME/lib中加载



【参考资料】

https://www.jianshu.com/p/d90e4430b0b9



