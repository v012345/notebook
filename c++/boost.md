## 目的
在 Windows 11 上使用 boost (Version 1.80.0) 库

## 环境
+ Visual Studio x64 2022
+ cmake
+ Visual Studio Code with "C/C++ Extension Pack" plugin

## 步骤
1. [官网下载 boost 源码](https://www.boost.org/users/history/version_1_80_0.html)
2. 下载好的 `boost_1_80_0.zip` 文件解压到 `C` 盘根目录 , 名字直接叫 `boost_1_80_0` 好了
3. 伪 bash 
    ```shell
    $ cd c:/boost_1_80_0
    $ ./bootstrap vc143 # vc143 对应 vs2022
    $ ./b2
    ```
4. 上一步可能会有一些 failed target 产生 , 先不管 , 因为我也不知道为什么 , 先能跑起来再说吧
5. `CMakeList.txt` 的配置
    ```cmake
    cmake_minimum_required(VERSION 3.20.0)
    project(BoostTest)
    set(BOOST_ROOT "C:\\boost_1_80_0") # either set it here or from     the command line  
    # set(Boost_USE_STATIC_LIBS OFF) 
    # set(Boost_USE_MULTITHREADED ON)  
    # set(Boost_USE_STATIC_RUNTIME OFF) 
    find_package(Boost REQUIRED) # header only libraries must not be    added here
    add_executable(main main.cpp)
    
    target_include_directories(main PUBLIC ${Boost_INCLUDE_DIRS}) 
    target_link_libraries(main ${Boost_LIBRARIES})
    ```

