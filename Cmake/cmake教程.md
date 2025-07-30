
# 第一章. CMake 教程

## 1、 hello示例(基本)

本教程中的文件如下：

>  tree
> .
> ├── CMakelists.txt
> └── main.cpp
>
> 0 directories, 2 files

- **CMakeLists.txt** - 包含您希望运行的 CMake 命令
- **main.cpp** 一个简单的“Hello World”cpp 文件。

### 1.1 **CMakeLists.txt**

CMakeLists.txt 文件用于存储所有 CMake 命令。在文件夹中运行 CMake 时，它会查找此文件，如果该文件不存在，CMake 将返回错误并退出。

### 1.2 最低 CMake 版本

使用 CMake 创建项目时，可以指定支持的 CMake 最低版本。

```
cmake_minimum_required(VERSION 3.5)
```

### 1.3 项目

CMake 构建可以包含项目名称，以便在使用多个项目时更容易引用某些变量。

```
project (hello_cmake)
```

### 1.4 创建可执行文件

add_executable() 命令指定应从指定的源文件（在本例中为 main.cpp）构建可执行文件。add_executable() 函数的第一个参数是要构建的可执行文件的名称，第二个参数是要编译的源文件列表。

```
add_executable(hello_cmake main.cpp)
```

>[!tip]
>
>有些人会使用一种简写方式，让项目名称和可执行文件名称相同。这样，你就可以像下面这样指定 CMakeLists.txt 文件：
>
>```
>cmake_minimum_required(VERSION 2.6)
>project (hello_cmake)
>add_executable(${PROJECT_NAME} main.cpp)
>```
>
>在此示例中，project() 函数将创建一个变量 ${PROJECT_NAME}，其值为 hello_cmake。然后，该变量可以传递给 add_executable() 函数，以输出“hello_cmake”可执行文件。



### 1.5 外部源代码构建

使用源外构建，您可以创建一个单独的构建文件夹，该文件夹可以位于文件系统的任何位置。所有临时构建文件和目标文件都位于此目录中，从而保持源代码树的整洁。要创建源外构建，请在构建文件夹中运行 cmake 命令，并将其指向包含根 CMakeLists.txt 文件的目录。如果您想使用源外构建从头开始重新创建 cmake 环境，只需删除构建目录，然后重新运行 cmake 即可。

> cmake ..
> -- The C compiler identification is GNU 11.4.0
> -- The CXX compiler identification is GNU 11.4.0
> -- Detecting C compiler ABI info
> -- Detecting C compiler ABI info - done
> -- Check for working C compiler: /usr/bin/cc - skipped
> -- Detecting C compile features
> -- Detecting C compile features - done
> -- Detecting CXX compiler ABI info
> -- Detecting CXX compiler ABI info - done
> -- Check for working CXX compiler: /usr/bin/c++ - skipped
> -- Detecting CXX compile features
> -- Detecting CXX compile features - done
> -- Configuring done
> -- Generating done
> -- Build files have been written to: /home/zlrobot/workspace/cmakeSpace/20250730/hello/build
> zlrobot@zl:~/workspace/cmakeSpace/20250730/hello/build$ make
> [ 50%] Building CXX object CMakeFiles/hello_cmake.dir/main.cpp.o
> [100%] Linking CXX executable hello_cmake
> [100%] Built target hello_cmake
> zlrobot@zl:~/workspace/cmakeSpace/20250730/hello/build$ ls-l
> ls-l: command not found
> zlrobot@zl:~/workspace/cmakeSpace/20250730/hello/build$ ls -l
> total 1340
> -rw-r--r-- 1 zlrobot zlrobot   14133 Jul 30 20:23 CMakeCache.txt
> drwxr-xr-x 6 zlrobot zlrobot    4096 Jul 30 20:23 CMakeFiles
> -rw-r--r-- 1 zlrobot zlrobot    5303 Jul 30 20:23 Makefile
> -rw-r--r-- 1 zlrobot zlrobot    1674 Jul 30 20:23 cmake_install.cmake
> -rwxr-xr-x 1 zlrobot zlrobot   16528 Jul 30 20:23 hello_cmake
> -rw-r--r-- 1 zlrobot zlrobot 1318204 Apr 21  2020 libssl1.1_1.1.1f-1ubuntu2_amd64.deb
> zlrobot@zl:~/workspace/cmakeSpace/20250730/hello/build$
> zlrobot@zl:~/workspace/cmakeSpace/20250730/hello/build$
> zlrobot@zl:~/workspace/cmakeSpace/20250730/hello/build$ ./hello_cmake
> hello Cmake!
> zlrobot@zl:~/workspace/cmakeSpace/20250730/hello/build$

## 2、包含头文件的hello示例

本教程中的文件包括：

```
.
├── CMakeLists.txt
├── build
├── include
│   └── Hello.h
└── src
    ├── hello.cpp
    └── main.cpp

3 directories, 4 files
```

- CMakeLists.txt- 包含您希望运行的 CMake 命令。
- include/Hello.h 要包含的头文件。
- /src/Hello.cpp 要编译的源文件。
- src/main.cpp 包含 main 的源文件。

**CMakeLists.txt**

```c++
# Set the minimum version of CMake that can be used

# To find the cmake version run

# $ cmake --version

cmake_minimum_required(VERSION 3.5)

# Set the project name

project (hello_headers)

# Create a sources variable with a link to all cpp files to compile

set(SOURCES
    src/Hello.cpp
    src/main.cpp
)

# Add an executable with the above sources

add_executable(hello_headers ${SOURCES})

# Set the directories that should be included in the build command for this target

# when running g++ these will be included as -I/directory/path/

target_include_directories(hello_headers
    PRIVATE 
        ${PROJECT_SOURCE_DIR}/include
)
```

### 2.1 概念

#### (1)目录路径

CMake 语法指定了许多变量，可用于帮助在项目或源代码树中查找有用的目录。其中包括：

| Variable                 | Info                                               |
| ------------------------ | -------------------------------------------------- |
| CMAKE_SOURCE_DIR         | 根源目录                                           |
| CMAKE_CURRENT_SOURCE_DIR | 如果使用子项目和目录，则为当前源目录。             |
| PROJECT_SOURCE_DIR       | 当前 cmake 项目的源目录。                          |
| CMAKE_BINARY_DIR         | 根二进制文件/构建目录。这是运行 cmake 命令的目录。 |
| CMAKE_CURRENT_BINARY_DIR | 您当前所在的构建目录。                             |
| PROJECT_BINARY_DIR       | 当前项目的构建目录。                               |

#### (2)源文件变量

创建一个包含源文件的变量可以让您更清楚地了解这些文件并轻松地将它们添加到多个命令中，例如 add_executable() 函数。

```
# Create a sources variable with a link to all cpp files to compile
set(SOURCES
    src/Hello.cpp
    src/main.cpp
)

add_executable(${PROJECT_NAME} ${SOURCES})
```





