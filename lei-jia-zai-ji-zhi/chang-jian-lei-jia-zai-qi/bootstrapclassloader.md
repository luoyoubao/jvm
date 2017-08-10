###BootstrapClassLoader###
引导类加载器(Bootstrap Classloader)会读取{JRE_HOME}/lib下的jar包和配置，然后将这些系统类加载到方法区内:
|||
|:--:|:--:|







rt.jar	        运行环境包，rt即runtime，J2SE 的类定义都在这个包内
charsets.jar	字符集支持包
jce.jar	        是一组包，它们提供用于加密、密钥生成和协商以及 Message Authentication Code（MAC）算法的框架和实现
jsse.jar	    安全套接字拓展包Java(TM) Secure Socket Extension
classlist	    该文件内表示是引导类加载器应该加载的类的清单
net.properties	JVM 网络配置信息