# cmake

## add_custom_command
自动触发
```cmake
if (MSVC)
  set(dlls reader edf)
  foreach(dll ${dlls})
    add_custom_command(
      TARGET test POST_BUILD
      COMMAND ${CMAKE_COMMAND} -E copy_if_different
              $<TARGET_FILE:${dll}>
              $<TARGET_FILE_DIR:test>
      COMMENT "Copying DLL to output directory"
    )
  endforeach()
endif()

```
## add_custom_target
手动触发，例如 make xxx
```cmake
add_custom_target(copy_dll
    ALL
    DEPENDS ${CMAKE_BINARY_DIR}/bin/mydll.dll
    COMMENT "Custom target to copy DLL files"
)
```

## WIN32,_WIN32,_WIN64
1. WIN32: 引入windows.h就会被定义，不能用做判断平台环境
2. _WIN32: 32位和64位都有
3. _WIN64: 64位才有

所以WIN32/_WIN32用做判断系统环境，_WIN64用作编译环境是32位还是64位