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