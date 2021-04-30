include_directories(${PROJECT_SOURCE_DIR}/mylib)

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

CONFIGURE_FILE(
	"${PROJECT_SOURCE_DIR}/config/config.hpp.in"
	"${PROJECT_SOURCE_DIR}/config/config.hpp"
)

option(USE_MYMATH
	ON
	)
IF(USE_MYMATH)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/mylib)
ENDIF(USE_MYMATH)

AUX_SOURCE_DIRECTORY(./ DIR_SRCS)

add_executable(demo5  ${DIR_SRCS})

target_link_libraries(demo5 Mylib)

