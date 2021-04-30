cmake_minimum_required(VERSION 2.6)
project(demo2)
# 
#add_executable(demo2 main.cpp mymath.cpp)
AUX_SOURCE_DIRECTORY(./ DIR_SRCS)
add_executable(demo2 main.cpp ${DIR_SRCS})


