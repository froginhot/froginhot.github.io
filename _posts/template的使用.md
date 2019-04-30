# C++中的map

### 简介

* 是STL的一个关联容器，提供一对一（**key：value**）的数据处理；

* map内部自建一颗红黑树（严格意义的平衡二叉树），对数据进行**自动排序**；
* 增加和删减节点对迭代器影响很小；
* 对于迭代器，可以修改关键字的值，但**不能修改key**;

* 根据key快速查找记录，复杂度为log(N);

### 使用

* 使用map得包含map类所在的头文件：`#include <map>`

* map实例化：`std:map<int,string> personnel;`

* 方便使用，可以利用typedef:

  ```
  typedef map<int,CString> UDT_MAP_INT_CSTRING;
  UDT_MAP_INT_CSTRING enumMap;
  ```

### 数据插入

1. insert函数 插入pair数据

```
map<int, string> mapStudent;  
mapStudent.insert(pair<int, string>(1, "student_one"));  
```

2. insert插入value_type数据

```
map<int, string> mapStudent;    
mapStudent.insert(map<int, string>::value_type (1, "student_one"));  
```

3. 数组方式插入数据

```
map<int, string> mapStudent;  
mapStudent[1] = "student_one";  
```

* 1和2在效果上是完成一样的，用 insert 函数插入数据，涉及到集合的唯一性，即当 map 中有这个关键字时，insert 操作是**插不了**的;
* 3的数组方式就不同了，它可以**覆盖**以前该关键字对 应的值。

### 数据查找

通过find()方法，

* 传入参数是要查找的 key；
* 返回的一个迭代器，当数据出现时，它返回数据所在位置的迭代器，没有要查找的数据，则返回 end 函数返回的迭代器。

* 通过 map 对象的方法获取的 iterator 数据类型是一个 **std::pair 对象**，包括两个数据 **iterator->first** 和 **iterator->second** 分别代表关键字和存储的数据。

```
map<int, string>::iterator iter;   
iter = mapStudent.find(1);  
  if(iter != mapStudent.end())  //判断是否找到要查找的key
       cout<<"Find, the value is"<<iter->second<<endl;  
  else  
       cout<<"Do not Find"<<endl;  
```

