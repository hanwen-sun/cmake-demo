#  最低版本号要求
cmake_minimum_required(VERSION 2.8)

# 项目信息  表示该项目名称为Demo1;
project(Demo4)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

option(USE_MYMATH "Use provided math implementation" ON)
#加入一个配置头文件config.h, 用于处理CMake对源码的设置;
configure_file(              # project_source_dir & binary/dir 都默认最近的定义project()的目录, 即当前目录;
    "${PROJECT_SOURCE_DIR}/config.h.in"
    "${PROJECT_BINARY_DIR}/config.h"
)
message("PROJECT_SOURCE_DIR: ${PROJECT_SOURCE_DIR}")
# 这里的configure_file和option结合使用, 先在.h.in文件中预定义, 经过实际的option写入config.h
# option命令添加了一个use_mymath选项, 且默认为on;  


#是否加入MathFunction库
if (USE_MYMATH)
  include_directories ("${PROJECT_SOURCE_DIR}/math")
  add_subdirectory (math)  
  set (EXTRA_LIBS ${EXTRA_LIBS} mathfunctions)
endif (USE_MYMATH)

message("extra_libs: ${EXTRA_LIBS}")
# aux_source_directory(<dir> <variable>)   
# 查找指定目录下的所有源文件, 并将名称保存到指定变量中;
aux_source_directory(. DIR_SRCS)

# 指定生成目标   将main.cc的源文件编译为名为Demo的可执行文件;
add_executable(Demo ${DIR_SRCS})

#添加链接库 (Demo项目需要添加一个链接库)  在子目录中生成的
target_link_libraries(Demo ${EXTRA_LIBS})