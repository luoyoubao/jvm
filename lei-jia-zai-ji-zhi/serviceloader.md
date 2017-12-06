ServiceLoader用来获取一个接口的子类

用java.util.ServiceLoader\#load\(java.lang.Class&lt;S&gt;\) 方法，但是直接使用该方法也是不能获取到给定接口所有的子类的。

需要接口的子类以配置的方式主动注册到一个接口上，才能使用ServiceLoader进行加载到子类，并且子类需要有一个无参构造方法，用于被ServiceLoader进行实例化

