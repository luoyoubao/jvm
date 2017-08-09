Class文件是以8位字节为基础单位的二进制流

#### 字节存储方式

大端和小端\(Big endian and Little endian\):对于整型、长整型等数据类型，Big endian 认为第一个字节是最高位字节（按照从低地址到高地址的顺序存放数据的高位字节到低位字节）；而 Little endian 则相反，它认为第一个字节是最低位字节（按照从低地址到高地址的顺序存放据的低位字节到高位字节）

#### 构成

** 无符号数**

* u1：1个字节
* u2：2个字节
* u4：4个字节
* u8：8个字节
* 可描述数字、索引引用、数量值或UTF-8编码的字符串值
  ** 表 **
  由多个无符号数或者其他表作为数据项构成的复合数据类型\("\_info"结尾\)，用于描述有层次关系的复合结构的数据，整个Class文件本质上就是一张表

#### class字节码文件结构
```
class {
    u4                magic;
    u2                minor_version;
    u2                major_version;
    u2                constant_pool_count;
    cp_info           constant_pool[constant_pool_count - 1];
    u2                access_flags;
    u2                this_class;
    u2                super_class;
    u2                interfaces_count;
    interfaces        interfaces[interfaces_count];
    u2                fields_count;
    field_info        field[fields_count];
    u2                methods_count;
    method_info       methods[methods_count];
    u2                attributes_count;
    attribute_info    attributes[attributes_count];
}
```

![](/assets/201708092326.png)



