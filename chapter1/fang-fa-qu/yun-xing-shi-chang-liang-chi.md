### 运行时常量池\(Runtime Constant Pool\)

用于存放编译期生成的各种字面量和符号引用；JAVA虚拟机规范未对运行时常量池做任何细节要求

#### 方法区运行时常量池与Class文件常量池的区别

运行时常量池具备动态性，JAVA语言并不要求常量必须在编译期产生\(即并非预置入Class文件中的常量池的内容才能进入方法区运行时常量池\)，运行期间也可能将新的常量放入运行时常量池\(如String.intern\(\)方法\)

#### 特性

* new String\("Hello World"\)并不放在常量池
* 运行时常量池是字节码文件中常量池表的运行时表现形式
* 运行时常量池中包含多种不同的常量，如编译期就已经明确的数值字面量，运行期解析后获得的方法或者字段引用
* 当类装载器成功将一个类或接口装载进JVM后，就会创建与之对应的运行时常量池



