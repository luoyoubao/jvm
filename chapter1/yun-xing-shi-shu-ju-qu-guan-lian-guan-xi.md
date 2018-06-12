##### 示例分析：

```
//源代码 Test.java  
package edu.hr.jvm;  
  
import edu.hr.jvm.bean;  
public class Test{  
       public static void main(String[] args){  
               Act act=new Act();  
               act.doMathForever();  
       }  
}  
  
//源代码 Act.java  
package edu.hr.jvm.bean;  
  
public class Act{  
       public void doMathForever(){  
              int i=0;  
              for(;;){  
                     i+=1;  
                     i*=2;   
              }  
       }  
}

作者：动脑学院安卓学院
链接：https://www.jianshu.com/p/e3394c1c0b56
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



