# subdir/CMakeLists.txt

get_directory_property(INCLUDE_DIRS INCLUDE_DIRECTORIES)
message(STATUS "subdir--property--INCLUDE_DIRECTORIES: ${INCLUDE_DIRS}")

# This will affect the parent scope's targets as well
include_directories(${CMAKE_SOURCE_DIR}/include)

get_directory_property(INCLUDE_DIRS INCLUDE_DIRECTORIES)
message(STATUS "subdir--property--INCLUDE_DIRECTORIES: ${INCLUDE_DIRS}")

# Define the target in the subdirectory
add_executable(subdir_target subdir_file.cpp)
