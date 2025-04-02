# 结论

> The include directories are added to the INCLUDE_DIRECTORIES directory property for the current CMakeLists file. They are also added to the INCLUDE_DIRECTORIES target property for each target in the current CMakeLists file. The target property values are the ones used by the generators.

- 在根目录的 CMakeLists.txt 中添加 include_directories 会影响到当前目录和子目录的 targets 和 directory `INCLUDE_DIRECTORIES` property
- 在子目录的 CMakeLists.txt 中添加 include_directories 不会影响父目录的 targets 和 directory `INCLUDE_DIRECTORIES` property

# 测试

```bash
cd tests/include_directories
mkdir build
cd build
cmake ..
make VERBOSE=1
```

输出结果：

```bash
root--property--INCLUDE_DIRECTORIES: 
-- subdir--property--INCLUDE_DIRECTORIES: 
-- subdir--property--INCLUDE_DIRECTORIES: /Users/<username>/Archive/nova/repos/test_cmake/tests/include_directories/include
-- root--property--INCLUDE_DIRECTORIES:
```

切实说明在子目录的 CMakeLists.txt 中添加 include_directories 不会影响父目录的 targets 和 directory `INCLUDE_DIRECTORIES` property