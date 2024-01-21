# Minimal CMakeLists.txt for project insight features in CLion.

# The project should still be built with `build.bat` after
# running `vcvarsall.bat` to make the Visual Studio toolchain available.

# This file is only here to placate CLion since it can't introspect
# the source tree to generate project info. Ultimately I should probably
# just make the time to learn 4coder and use that instead.

# A hand-crafted `compile_commands.json` file also works to generate
# project info, but those require absolute directory paths such that
# they need to be custom to each developer's file system and so
# shouldn't be version controlled

# Other minimal IDEs don't correctly generate project data
# from this file, and require the `compile_commands.json` file instead,
# but **not** one generated from this file via `set(CMAKE_EXPORT_COMPILE_COMMANDS ON)`

# To get this project to load nicely in VSCode:
# - copy `compile_commands.example.json` and rename it to `compile_commands.json`
# - replace "C:\\absolute\\path\\to\\project\\raddebugger" in each "directory" entry
#   with the correct path to the project root for your system (keep "\\build" at the end)

cmake_minimum_required(VERSION 3.15)
project(raddebugger)

include_directories(src/ local/)

# main executable
add_executable(${PROJECT_NAME} src/raddbg/raddbg_main.cpp)

# supplemental executables
add_executable(raddebug_dump       src/raddbg_dump/raddbg_dump.c)
add_executable(raddebug_from_pdb   src/raddbg_convert/pdb/raddbg_from_pdb_main.c)
add_executable(raddebug_from_dwarf src/raddbg_convert/dwarf/raddbg_from_dwarf.c)
