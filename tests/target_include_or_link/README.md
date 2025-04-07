# 结论

## target_include_or_link 会设置哪些属性

- 头文件路径
    - INCLUDE_DIRECTORIES
    - INTERFACE_INCLUDE_DIRECTORIES
- 库依赖
    - LINK_LIBRARIES
    - INTERFACE_LINK_LIBRARIES

##  PUBLIC/PRIVATE/INTERFACE 的作用

- PRIVATE: `INCLUDE_DIRECTORIES` 和 `LINK_LIBRARIES`
- INTERFACE: `INTERFACE_INCLUDE_DIRECTORIES` 和 `INTERFACE_LINK_LIBRARIES`
- PUBLIC: PRIVATE 和 INTERFACE 的并集

# 测试

```bash
cmake -B build -S .
```

输出：

```bash
PRIVATE include directories: /Users/<username>/Archive/nova/repos/test_cmake/tests/target_include_or_link/private_include;/Users/<username>/Archive/nova/repos/test_cmake/tests/target_include_or_link/public_include
PUBLIC/INTERFACE include directories: /Users/<username>/Archive/nova/repos/test_cmake/tests/target_include_or_link/public_include;/Users/<username>/Archive/nova/repos/test_cmake/tests/target_include_or_link/interface_include
PRIVATE link libraries: OtherPrivateLib;OtherPublicLib
PUBLIC/INTERFACE link libraries: OtherPublicLib;OtherInterfaceLib
--------------------------------
PRIVATE include directories: /Users/<username>/Archive/nova/repos/test_cmake/tests/target_include_or_link/private_include;/Users/<username>/Archive/nova/repos/test_cmake/tests/target_include_or_link/public_include
PUBLIC/INTERFACE include directories: /Users/<username>/Archive/nova/repos/test_cmake/tests/target_include_or_link/public_include;/Users/<username>/Archive/nova/repos/test_cmake/tests/target_include_or_link/interface_include
PRIVATE link libraries: OtherPrivateLib;OtherPublicLib
PUBLIC/INTERFACE link libraries: $<LINK_ONLY:OtherPrivateLib>;OtherPublicLib;OtherInterfaceLib
```

可以验证上述的结论。

# 为什么 STATIC + PRIVATE link 会有 $<LINK_ONLY:OtherPrivateLib>？

这部分：

```bash
PUBLIC/INTERFACE link libraries: $<LINK_ONLY:OtherPrivateLib>;OtherPublicLib;OtherInterfaceLib
```

回答，参考 [How Link Only Really Works](https://discourse.cmake.org/t/how-link-only-really-works/10673)

这是因为静态库（STATIC）的特殊性质导致的。静态库本质上只是一个目标文件的归档，它本身并没有真正的链接阶段。当其他目标使用这个静态库时，需要将所有依赖都传递给最终的可执行文件或动态库。

当我们使用 `PRIVATE` 依赖时，按照定义这个依赖不应该被传递给使用该静态库的目标。但是静态库的特性决定了我们必须传递这个依赖，否则最终链接会失败。为了解决这个矛盾，CMake 引入了 `$<LINK_ONLY:...>` 机制。

`$<LINK_ONLY:...>` 的作用是：
1. 允许依赖在链接阶段被传递（确保链接成功）
2. 但不传递该依赖的其他属性（如头文件路径、编译定义等）

这样就既保证了静态库的正确链接，又遵守了 `PRIVATE` 依赖的语义 - 不暴露实现细节给使用者。
