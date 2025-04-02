# CMakeLists.txt at the root level

cmake_minimum_required(VERSION 3.10)
project(IncludeDirectoriesExample)

get_directory_property(INCLUDE_DIRS INCLUDE_DIRECTORIES)
message(STATUS "root--property--INCLUDE_DIRECTORIES: ${INCLUDE_DIRS}")

# Add subdirectory
add_subdirectory(subdir)

get_directory_property(INCLUDE_DIRS INCLUDE_DIRECTORIES)
message(STATUS "root--property--INCLUDE_DIRECTORIES: ${INCLUDE_DIRS}")

# Define the top-level target
add_executable(root_target main.cpp)
