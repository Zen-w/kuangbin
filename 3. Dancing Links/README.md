# 专题三 舞蹈链 Dancing Links

Dancing Links 舞蹈链算法，通俗点说，我认为是采用交叉十字循环链表结构的回溯，相比普通回溯，其通过指针的使用，很大程度上提升了搜索的效率。

该算法用来实现求解“精准覆盖”（01矩阵取某些行，使得每行每列仅存在一个 1，其余全 0）。

模板及示例可见 A.cpp，使用时，将不同题目的情况处理为 01 矩阵，（基本上）只用加上预处理和修改 dance 方法。

该目录下 舞蹈链.cpp 为学习该算法时手写的基于指针（非数组）的实现，但很无奈错误有点多，跑不起来...

参考讲解：https://www.cnblogs.com/grenet/p/3145800.html