### 74.2 CMake Configuration

```cmake
if(WIN32)
    add_definitions(-DWINDOWS_BUILD)
elseif(UNIX)
    add_definitions(-DLINUX_BUILD)
endif()
```