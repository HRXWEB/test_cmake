# PUBLIC_HEADER 测试说明

## 测试目的
测试CMake中`PUBLIC_HEADER`属性的作用及其对include路径的影响。

## 测试配置
在`src/CMakeLists.txt`中设置了：
```cmake
set_target_properties(MyLib PROPERTIES PUBLIC_HEADER mylib.h)
```

## PUBLIC_HEADER的主要用途
`PUBLIC_HEADER`属性主要与`install`命令配合使用：
1. 当执行`install(TARGETS MyLib ...)`时，CMake会自动将`PUBLIC_HEADER`指定的头文件安装到指定位置
2. 典型的安装配置示例：
```cmake
install(TARGETS MyLib
    LIBRARY DESTINATION lib
    PUBLIC_HEADER DESTINATION include
)
```
这会将`mylib.h`安装到`include`目录下

## 测试结果

### PUBLIC_HEADER的作用
1. `PUBLIC_HEADER`属性主要用于指定库的公共头文件，这些头文件会在安装时被复制到指定位置
2. 从CMake输出可以看到，设置`PUBLIC_HEADER`后：
   - `MyLib_PUBLIC_HEADER`被正确设置为`mylib.h`
   - `MyLib_INCLUDE_DIRECTORIES`和`MyLib_INTERFACE_INCLUDE_DIRECTORIES`都是`NOTFOUND`
   - `MyLib_INTERFACE_LINK_LIBRARIES`也是`NOTFOUND`

### 重要发现
1. **PUBLIC_HEADER不会自动设置include路径**
   - 即使设置了`PUBLIC_HEADER`，编译器仍然无法找到头文件
   - 编译错误显示：`fatal error: 'mylib.h' file not found`

2. **需要额外配置**
   - 要使用库的头文件，仍然需要：
     - 要么使用`target_include_directories()`设置include路径
     - 要么在链接库时使用`PUBLIC`关键字传递include路径

## 结论
1. `PUBLIC_HEADER`属性主要用于安装时的头文件管理，不会自动处理编译时的include路径
2. 不能依赖`PUBLIC_HEADER`来解决头文件查找问题
3. 要正确使用库的头文件，需要显式配置include路径或使用正确的target属性
4. `PUBLIC_HEADER`的主要用途是与`install`命令配合，用于管理库的公共头文件的安装位置 