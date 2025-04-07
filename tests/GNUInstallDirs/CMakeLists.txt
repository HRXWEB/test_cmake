cmake_minimum_required(VERSION 3.10)

project(test_GNUInstallDirs)

include(GNUInstallDirs)

# print all cached variables defined by GNUInstallDirs
# prefix of all variables is `CMAKE_INSTALL_`
get_cmake_property(CACHE_VARIABLES CACHE_VARIABLES)
foreach(CACHE_VARIABLE IN LISTS CACHE_VARIABLES)
    if ("${CACHE_VARIABLE}" MATCHES "^CMAKE_INSTALL_")
        message("${CACHE_VARIABLE} = ${${CACHE_VARIABLE}}")
    endif()
endforeach()


