# Cached Variables defined by GNUInstallDirs

```bash
cd tests/GNUInstallDirs
mkdir build
cd build
cmake ..
```

输出结果（截取）：

```bash
CMAKE_INSTALL_BINDIR = bin
CMAKE_INSTALL_DATADIR = share
CMAKE_INSTALL_DATAROOTDIR = share
CMAKE_INSTALL_DOCDIR = share/doc/test_GNUInstallDirs
CMAKE_INSTALL_INCLUDEDIR = include
CMAKE_INSTALL_INFODIR = share/info
CMAKE_INSTALL_LIBDIR = lib
CMAKE_INSTALL_LIBEXECDIR = libexec
CMAKE_INSTALL_LOCALEDIR = share/locale
CMAKE_INSTALL_LOCALSTATEDIR = var
CMAKE_INSTALL_MANDIR = share/man
CMAKE_INSTALL_NAME_TOOL = /opt/homebrew/anaconda3/bin/install_name_tool
CMAKE_INSTALL_OLDINCLUDEDIR = /usr/include
CMAKE_INSTALL_PREFIX = /usr/local
CMAKE_INSTALL_RUNSTATEDIR = var/run
CMAKE_INSTALL_SBINDIR = sbin
CMAKE_INSTALL_SHAREDSTATEDIR = com
CMAKE_INSTALL_SYSCONFDIR = etc
```

# 参考

- [GNUInstallDirs](https://github.com/Kitware/CMake/blob/master/Modules/GNUInstallDirs.cmake)
- [CMake Documentation](https://cmake.org/cmake/help/latest/module/GNUInstallDirs.html)


