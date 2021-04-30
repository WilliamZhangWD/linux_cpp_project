cmake_minimum_required(VERSION 2.6)

project(demo3)

add_subdirectory(./mylib)

AUX_SOURCE_DIRECTORY(./ DIR_SRCS)

add_executable(demo3 main.cpp ${DIR_SRCS})

target_link_libraries(demo3 Mylib)