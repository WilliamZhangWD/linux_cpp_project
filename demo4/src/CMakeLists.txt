include_directories(${PROJECT_SOURCE_DIR}/mylib)

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

AUX_SOURCE_DIRECTORY(./ DIR_SRCS)

add_executable(demo4  ${DIR_SRCS})

target_link_libraries(demo4 Mylib)

