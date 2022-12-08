
aux_source_directory(. DIR_LIB_SRCS)

# 生成链接库  把当前目录下的源文件编译成静态链接库;
add_library(mathfunctions ${DIR_LIB_SRCS})    # 注意这里没有 ','
# 这里会在math文件夹下生成libmathfunctions.a 即静态链接库;