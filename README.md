demo1
单文件
先执行cmake ./
再执行make
后执行运行结果./zwd1 5 2 

重新make前需要make clean

demo2 
多文件 单目录
添加依赖 add_executable(demo2 main.cpp mymath.cpp) 
就是在main.cpp 后面添加mymath.cpp。那么如果依赖很多怎么办，不可能一个一个输入。
使用AUX_SOURCE_DIRECTORY(文件夹 变量名)   
AUX_SOURCE_DIRECTORY(./ DIR_SRCS)
add_executable(demo2  ${DIR_SRCS})

deom3
多文件 多目录
在子目录里：
也写CMakeLists.txt
使用:
aux_source_directory(. DIR_LIB_SRCS ) 将当前文件夹下的文件名保存在DIR_LIB_SRCS变量中
add_library(Mylib ${DIR_LIB_SRCS}) 将该文件夹中的文件添加进静态库。 Mylib是我起的名字
或 使用add_library(Mylib SHARED ${DIR_LIB_SRCS}) 将该文件夹中的文件添加进动态库。
在顶层目录里：
add_subdirectory(./mylib)
target_link_libraries(demo3 Mylib)

demo4
多目录 标准工程（src、build）
src里：
main.cpp
CMakeLists.txt
include_directories(${PROJECT_SOURCE_DIR}/mylib) #添加库头文件搜索路径 ${PROJECT_SOURCE_DIR}代表根路径，此处等同于"."
build存放编译生成的文件。

更近一步，mylib的静态库libMylib.a还和其他文件在一起（更标准应该是在lib文件夹）;
src下的可执行二进制文件（demo）也还和其他文件在一起（更标准应该是在bin文件夹）;
mylib文件夹的cmakelists.txt:set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib) PROJECT_BINARY_DIR=build
src文件夹的cmakelists.txt:SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

demo5
自定义编译选项
1.根目录新建config文件夹，其中新建config.hpp.in文件
2.src的cmakelists.txt

进入到build，ccmake ..或ccmake .
设置好后，c-g。再在build中make

添加opencv :
find_package(OpenCV REQUIRED)
...
target_link_libraries(aruco_temp lib1 lib2 ... ${OpenCV_LIBS})
学习笔记：find_package如何找到库的？
使用的是pkg-config
命令行：pkg-config --cflags opencv
命令行：pkg-config --libs opencv

每次需要 include "../lib/.."太烦啦。使用include_directories("../lib" "../config")处理



