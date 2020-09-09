# C/C++ Lang Specific Requirements

These requirements are intended specifically for the C/C++ based projects.

### Documentation

##### [C.D.NAMING]
Following naming conventions should be used.

| Symbol Kind   | Prefix         | Style  | Suffix |
| ------------- |-------------| -----| -----|
| Namespaces | - | camelCase | - |
| Macros | \_\_M\_ | SCREAMING_SNAKE_CASE | - |
| Classes And Structs | *(optional/recomemnded)* prj short name | PascalCase | - |
| Enums | E_ | PascalCase | - |
| Enumerators | - | PascalCase | - |
| Typedefs | tdef_ | snake_case | - |
| Unions | u_ | PascalCase | - |
| Methods | - | camelCase | - |
| Fields | m_ | PascalCase | - |
| Parameters | par | PascalCase | - |
| Local Variables | _ | snake_case | - |

##### [C.D.TOOLS]
For C and C++ powered projects it is recommended to use [Doxygen](https://www.doxygen.nl/index.html) for documentation purposes.

##### [C.D.1]
All developer-made macros definitions should be referenced in the special file *MACROS_DEFS.md* placed in the repository root. Each definition file must follow the format:

````
### Macros definitions
| Macro name   | File path        | Purpose                         |
| ------------ | ---------------- | ------------------------------- |
| \__M_EXAMPLE | source/example.h | Example reason to use the macro |
| etc...       |                  |                                 |
````

##### [C.D.2]
All developer-made typedef definitions should be referenced in the special file *TYPEDEF_DEFS.md* placed in the repository root. Each definition file must follow the format:

````
### Macros definitions
| Typedef name | File path            | Purpose                           |
| ------------ | -------------------- | --------------------------------- |
| tdef_example | source/tdefExample.h | Example reason to use the typedef |
| etc...       |                      |                                   |
````

##### [C.D.3]
All developer-made meta-programming (template incl.) code should be referenced and additionally documented in the special file *METAPROGRAMMING.md* placed in the repository root. Each definition file must follow the format:

````
### Meta-Programming definitions

#### Meta Programming Def Example 1

Description and Purpose goes here...
...

| Source Files Paths | Purpose            | 
| ------------------ | ------------------ | 
| meta_example.h     | Intended for...    | 
| etc...             |                    | 

etc...
````

##### [C.D.4]
All developer-made raw pointers should be referenced in the special file *RAW_PTRS.md* placed in the repository root. Each definition file must follow the format:

````
### Raw pointers
| Raw Ptr Name | File path            | Purpose                           | Context                     | Mem Leak Protection      |
| ------------ | -------------------- | --------------------------------- | --------------------------- | ------------------------ |
| _rawPtrEx    | source/tRawPtrEx.h   | Example reason to use the typedef | Func ```void doExample()``` | Free in the same context |
| etc...       |                      |                                   |                             |                          |
````

### Build

##### [C.B.TOOLS]
[CMake](https://cmake.org) should be used for the build files generation process and project dependencies + configuration manager. 

##### [C.B.TOOLS.DEFAULT]
The default build config is *Debug* with all standard compiler warnings enabled. The following commands are executed during the default build:
``` bash
mkdir <prj_name>_build_debug 
cd <prj_name>_build_debug
cmake .. -DCMAKE_BUILD_TYPE=Debug
cmake --build build -DCMAKE_BUILD_TYPE=Debug
```

##### [C.B.1]
It is preferred, that the build process shouldn't provide any warnings during the standard build. If it's needed, warnings should be suppressed (in *CMakeLists.txt*). For example:

``` CMake
target_compile_definitions(TARGET PUBLIC /wdNNNN)
#where NNNN is the warning id
```

##### [C.B.2]
Project version should be always specified and updated in *CMakeLists.txt*, e.g.

``` CMake
SET(VERSION_MAJOR 1)
SET(VERSION_MINOR 0)
SET(VERSION_PATCH 0)
```


##### [C.B.3]
Each project might generate the version number based on the last commit and version parameters set by the build system. For the CMake you can use the Ignix-CMake-Submodules repo and the following template.

``` C
Version.h
extern const char GIT_SHA1[];
extern const char CMAKE_VER_MAJOR[];
extern const char CMAKE_VER_MINOR[];
extern const char CMAKE_VER_PATCH[];
---
Version.cpp.in
const char GIT_SHA1[] = "@GIT_SHA1@";
const char CMAKE_VER_MAJOR[] = "@PROJ_VERSION_MAJOR@";
const char CMAKE_VER_MINOR[] = "@PROJ_VERSION_MINOR@";
const char CMAKE_VER_PATCH[] = "@PROJ_VERSION_PATCH@";
```

``` CMake
CMakeLists.txt

add_custom_target(update_version ALL
		COMMAND ${CMAKE_COMMAND} -DGIT_SHA1="${GIT_SHA1}" -DPROJ_VERSION_MAJOR="${VERSION_MAJOR}" -DPROJ_VERSION_MINOR="${VERSION_MINOR}" -DPROJ_VERSION_PATCH="${VERSION_PATCH}" -P "${CMAKE_CURRENT_SOURCE_DIR}/external/ignix-cmake-submodules/Version.cmake"
	)
```

##### [C.B.4]
If the project has external resources for the build, during development build the resources folder should be symlinked, during the release build the resources folder should be cloned/copied. You can configure such behavior using CMake:

```` CMake
message("Resources will be symlinked")
if (WIN32)
    add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
            COMMAND "${CMAKE_CURRENT_SOURCE_DIR}/external/ignix-cmake-submodules/platform/windows/postbuild_res_export.bat"
                                    \"${EXPORT_RESOURCES_DIR}\" \"${RESOURCES_EXPORT}\" )
else()
    add_custom_command(TARGET ${PROJECT_NAME}
            POST_BUILD COMMAND ${CMAKE_COMMAND} -E create_symlink ${RESOURCES_EXPORT} ${EXPORT_RESOURCES_DIR})
endif()
````

For Windows it is needed to have separate script for the symlinking process (already included in Ignix-CMake-Submodules repo):

``` Bat
dir
echo %1
echo %2
mklink /J %1 %2
```

##### [C.B.5]
It is highly recommended to have at least 4 build configurations:
* Debug
* Release
* RelWithDebInfo
* MinSizeRel

### Code

##### [C.CODE.1]
All code should be located in namespaces, avoid using global namespace (except for DLL-export functions).

##### [C.CODE.2]
Implementation in *.c* or *.cpp* files is highly preferred, avoid placing it in the headers except for template meta-programming definitions.

##### [C.CODE.3]
One class per header-source pair is highly preferred.

##### [C.CODE.4]
It is highly recommended to separate data and logic.

### Features

##### [C.FEAT.1]
Avoid using multiple inheritances, use composition instead.

##### [C.FEAT.2]
Use ```override``` when overriding a virtual method.

##### [C.FEAT.3]
Reduce using macros definitions, use ``const`` and ``constexr`` if possible.

##### [C.FEAT.4]
Reduce using ``typedef``, use type aliases instead (if possible).

##### [C.FEAT.5]
Reduce using standard exceptions and exception handlers (``try {...} catch {...}``), write and prefer using non-except methods.

##### [C.FEAT.6]
Consider using smart pointers or references instead of raw pointers. Use raw pointers only if it has a very important purpose (e.g. performance-critical or memory-critical contexts).