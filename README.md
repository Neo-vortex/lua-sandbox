# Lua-Sandbox Repository

This repository contains the Lua programming language, an embeddable scripting language with a focus on simplicity and extensibility. Lua is commonly used as a lightweight scripting language in various domains, including game development, embedded systems, and scripting within larger applications.
This repo extend the lua language to be more friendly with different sandboxing use cases.


## Library Fusion System

In this repository, we have implemented a Library Fusion System, which allows you to selectively load specific Lua libraries based on a fusion value. The `luaL_openlibs` function has been modified to support this feature. Here's an example usage:

```c
#include "lua.h"
#include "lauxlib.h"

LUALIB_API void luaL_openlibs(lua_State* L, int fuse) {
  // Base library
  if (fuse == 0 || fuse % 2 == 1) {
    luaL_requiref(L, LUA_GNAME, luaopen_base, 1);
    lua_pop(L, 1);
  }

  // Package library
  if (fuse % 3 == 0) {
    luaL_requiref(L, LUA_LOADLIBNAME, luaopen_package, 1);
    lua_pop(L, 1);
  }

  // ... (other libraries)

  // Debug library
  if (fuse % 29 == 0) {
    luaL_requiref(L, LUA_DBLIBNAME, luaopen_debug, 1);
    lua_pop(L, 1);
  }
}
```


In this system, the fuse value determines which libraries are loaded. Each library is associated with a prime number, and if the fuse value is divisible by that prime number, the corresponding library is loaded.

Fuse Number - Libraries Loaded
Here is a table showing the valid fuse numbers and the corresponding libraries loaded:

| Fuse Number | Libraries Loaded |
|-------------|------------------|
| 0           | None             |
| 2           | Base             |
| 3           | Package          |
| 5           | Coroutine        |
| 7           | Table            |
| 11          | IO               |
| 13          | OS               |
| 17          | String           |
| 19          | Math             |
| 23          | UTF8             |
| 29          | Debug            |


Any combination of these would result in custom lib loading.
for example :

fuse = 2*3 would load base and package lib

Documentation
For detailed documentation and guides on using Lua, please refer to the official Lua website: https://www.lua.org

Contributions
Contributions to the Lua repository are welcome! If you find any issues or have suggestions for improvements, please submit a pull request or open an issue on the repository. Your contributions will help enhance the



