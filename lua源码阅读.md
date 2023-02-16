内存管理 就是 简单的 分配内存 , 我还不明白什么是 全局状态机
cast 要去理解
typedef 与 #define 的用法
LuaM_ 内存相关


lua_CFunction 在 c 中给 lua 注册函数时使用的 函数类型 用 typedef 定义的 typedef int (*lua_CFunction) (lua_State *L);
lua_Alloc 内存分配函数的指针  typedef void * (*lua_Alloc) (void *ud, void *ptr, size_t osize, size_t nsize);

CommonHeader  平铺成三个数据 , GCObject 的指针 , 两个无符号的 byte , 而这个 GCObject 正好也是包含这三个东西,所以如何一个结构体使用 CommonHeader 那个就比使用 GCObject* next的多出两个无符号的 byte.

Value Lua里的基本数据类型的一个 union体 , 要么是一个 lua_Number (是一个 double) n , 要么是一个 (lua_Number) (是一个long long) i , 要么是一个 lua_CFunction (就是上面的 lua_CFunction , 是一个返回为 int , 参数为 lua状态机的 函数指针) f , 要么是一个 void* p , 要么是一个目标 GCObject * gc 链.

TValue 就是上面的 Value 加一个 类型 (一个byte)

StkId 是一个指向 StackValue 的指针

StackValue 是一个 union 其中一个 tbclist  , 先不管 , 所以 StackValue 里面就是一个 TValue .

[lua源码编译及与C/C++交互调用细节剖析](https://zhuanlan.zhihu.com/p/395277828)

[Lua和C++交互 学习记录之一：C++嵌入脚本](https://www.cnblogs.com/chevin/p/5884657.html)

[子龙山人](https://zilongshanren.com/categories/lua/)

[lua_settable 函数详解](https://blog.csdn.net/tianyexing2008/article/details/126720901)