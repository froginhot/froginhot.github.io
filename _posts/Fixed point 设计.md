---
layout: post
title: "Matlab&Simulink中的Fixed point"
tags: [ fixed point]
comments: true
---
#### 设计思想

* 定点设计通过工具辅助完成；
* **定点设计vs浮点设计 testbend**搭建，覆盖工控内的取值范围；
* 根据推荐及效果进行修正；

#### Matlab中的定点设计

1. 编制好**主函数.m**和**测试.m**;

2. APP——代码生成——Fixed-point Converter（或者直接Matlab Coder）;

3. 选择函数文件：

![1556527129281](C:\Users\wanggeng\Pictures\typora\1556527129281.png)

4. 自己定义输入的数据类型和大小 || 通过**testbend.m**自动识别；

5. 设置：字长、圆整方法、溢出处理、仿真min/max的安全裕量等；

   ![1556527286136](C:\Users\wanggeng\Pictures\typora\1556527286136.png)

6. 分析：加载testbend.m、分析范围等
7. convert转换，并分析统计，修正或确定定点位Q；
8. 对比定点和浮点结果（已经做了吗？）

#### Simulink中的定点设计

1. 打开要定点化的模型（记得设计**原始模块**和**要定点的模块**（相同），并**对比结果模块**）
2. 对定点模块的子系统输入设置signal attributes里锁定输出不收定点工具影响

3. Analysis——Data Type Convert——Fixed point Tool

4. 选择要定点的模块，右键——Set as system under design——continue

![1556528712303](C:\Users\wanggeng\Pictures\typora\1556528712303.png)

5. 点击Fixed-Point Advisor，并按照提示，一步步检验（1.2.3的右键运行，避免一个个小支运行，太慢！！）
   * 出现问题可以modify all,或者按照提示，自己修改；

6. 点击范围搜集——simulate model——运行搜集——搜集浮点运行及结果

7. 数据类型设置——能否接受推荐定点——apply accepted data types——change all更新模型（**也可自己设置，记录数据，对比结果**）

![1556529286846](C:\Users\wanggeng\Pictures\typora\1556529286846.png)

8. 搜集定点数据及结果

![1556529784495](C:\Users\wanggeng\Pictures\typora\1556529784495.png)

9. 比对结果

![1556529920750](C:\Users\wanggeng\Pictures\typora\1556529920750.png)

10. 固定点模块代码生成

右键——Design Verifier——C/C++ Code——Build This Subsystem——弹窗Build

#### 参考

1.[MATLAB 定点算法的设计和实现](https://ww2.mathworks.cn/videos/introduction-to-fixed-point-algorithm-design-123499.html)

2.[MATLAB 和 Simulink 定点设计的快速入门](https://ww2.mathworks.cn/videos/introduction-to-fixed-point-designer-82572.html?elqsid=1556523042439&potential_use=Student)

