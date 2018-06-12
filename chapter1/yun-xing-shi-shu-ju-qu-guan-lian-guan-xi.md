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
```



