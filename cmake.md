---
title:	    cmake.md
subtitle:   Notes about creating cmake projects
author:		Reinaldo Molina
email:      rmolin88 at gmail dot com
date:       Tue May 29 2018 10:59
---

## Sample Project
- `wiki/CMakeLists.txt`

## Notes
- To see more of `make` output use `make VERBOSE=1`.

## Commands:
- They are set in the order that they normally go in the file:

### cmake_minimum_requiered(VERSION <version> [FATAL_ERROR])
- If you do not know what to make to. Make it to your current version.
- Should be specified in all your `CMakeLists.txt` files.

### project(<name>)
- You just name you project here.
- You can also specify your project language.
	- It defaults to `C and CXX`.
	- But you can say `JAVA or FORTRAN`
- If the name contains spaces needs to be surrounded in quotes.

### enable_testing()
- Should only be used in the top level `CMakeLists.txt`.
- Main thing it does is enables the `add_test()`.

### add_executable(<target> <sources...>)
- Tells cmake you want to make an executable and adds it as a target.
- `target` is the name you are giving the target.
- `sources` source files that will be used to make the target. No headers here.

### add_test(<testname> <executable> [<args...>])
- Depends on the previously mentioned `enable_testing` to be specified before this
command.
- Adds a test that will be run in the current directory by [CTest](https://gitlab.kitware.com/cmake/community/wikis/home#ctest).
- Tests are not run automatically. 

## Building
- CMake suggest always creating a `build` directory.

```
mkdir build
cd build
cmake -G <"Generetor"> <relative path to top level CMakeLists.txt>
```

- Example of last command:

`cmake -G "Unix Makefile" ..`

- To see available generators: `cmake --help`
