# 创建库目标
add_library(MyLib SHARED mylib.cpp)

# 设置公共头文件
set_target_properties(MyLib PROPERTIES PUBLIC_HEADER mylib.h)

get_target_property(MyLib_PUBLIC_HEADER MyLib PUBLIC_HEADER)
message("MyLib_PUBLIC_HEADER: ${MyLib_PUBLIC_HEADER}")
get_target_property(MyLib_INCLUDE_DIRECTORIES MyLib INCLUDE_DIRECTORIES)
message("MyLib_INCLUDE_DIRECTORIES: ${MyLib_INCLUDE_DIRECTORIES}")
get_target_property(MyLib_INTERFACE_INCLUDE_DIRECTORIES MyLib INTERFACE_INCLUDE_DIRECTORIES)
message("MyLib_INTERFACE_INCLUDE_DIRECTORIES: ${MyLib_INTERFACE_INCLUDE_DIRECTORIES}")
get_target_property(MyLib_INTERFACE_LINK_LIBRARIES MyLib INTERFACE_LINK_LIBRARIES)
message("MyLib_INTERFACE_LINK_LIBRARIES: ${MyLib_INTERFACE_LINK_LIBRARIES}")
