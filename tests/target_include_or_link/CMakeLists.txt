cmake_minimum_required(VERSION 3.10)

project(MyProject)

function(create_library name type)
    add_library(${name} ${type} ${ARGN})

    target_include_directories(${name}
        PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/private_include
        PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/public_include
        INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/interface_include
    )

    target_link_libraries(${name}
        PRIVATE OtherPrivateLib
        PUBLIC OtherPublicLib
        INTERFACE OtherInterfaceLib
    )
endfunction()

# 创建目标
create_library(MySharedLibrary SHARED mylib.cpp)
create_library(MyStaticLibrary STATIC mylib.cpp)

function(check_target_property name)
    get_target_property(${name}_include_dirs ${name} INCLUDE_DIRECTORIES)
    get_target_property(${name}_interface_include_dirs ${name} INTERFACE_INCLUDE_DIRECTORIES)
    get_target_property(${name}_link_libs ${name} LINK_LIBRARIES)
    get_target_property(${name}_interface_link_libs ${name} INTERFACE_LINK_LIBRARIES)

    message("PRIVATE include directories: ${${name}_include_dirs}")
    message("PUBLIC/INTERFACE include directories: ${${name}_interface_include_dirs}")
    message("PRIVATE link libraries: ${${name}_link_libs}")
    message("PUBLIC/INTERFACE link libraries: ${${name}_interface_link_libs}")
endfunction()

check_target_property(MySharedLibrary)
message("--------------------------------")
check_target_property(MyStaticLibrary)