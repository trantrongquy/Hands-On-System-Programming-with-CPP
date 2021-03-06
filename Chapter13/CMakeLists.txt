#
# Copyright (C) 2018 Rian Quinn <rianquinn@gmail.com>
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

# ------------------------------------------------------------------------------
# Header
# ------------------------------------------------------------------------------

cmake_minimum_required(VERSION 3.6)
project(chapter13)

include(ExternalProject)
find_package(Git REQUIRED)

set(CMAKE_CXX_STANDARD 17)

# ------------------------------------------------------------------------------
# Guideline Support Library
# ------------------------------------------------------------------------------

list(APPEND GSL_CMAKE_ARGS
    -DGSL_TEST=OFF
    -DCMAKE_INSTALL_PREFIX=${CMAKE_BINARY_DIR}
)

ExternalProject_Add(
    gsl
    GIT_REPOSITORY https://github.com/Microsoft/GSL.git
    GIT_SHALLOW 1
    CMAKE_ARGS ${GSL_CMAKE_ARGS}
    PREFIX ${CMAKE_BINARY_DIR}/external/gsl/prefix
    TMP_DIR ${CMAKE_BINARY_DIR}/external/gsl/tmp
    STAMP_DIR ${CMAKE_BINARY_DIR}/external/gsl/stamp
    DOWNLOAD_DIR ${CMAKE_BINARY_DIR}/external/gsl/download
    SOURCE_DIR ${CMAKE_BINARY_DIR}/external/gsl/src
    BINARY_DIR ${CMAKE_BINARY_DIR}/external/gsl/build
    UPDATE_DISCONNECTED 1
)

# ------------------------------------------------------------------------------
# Executable
# ------------------------------------------------------------------------------

include_directories(${CMAKE_BINARY_DIR}/include)

add_executable(example1 example1.cpp)
add_dependencies(example1 gsl)
target_link_libraries(example1)

# ------------------------------------------------------------------------------
# Snippets
# ------------------------------------------------------------------------------

function(snippet number)
    add_executable(snippet${number} scratchpad.cpp)
    target_compile_definitions(snippet${number} PRIVATE SNIPPET${number})
    target_link_libraries(snippet${number} pthread)
endfunction(snippet)

snippet(01)
snippet(02)
snippet(03)
snippet(04)
snippet(05)
snippet(06)
snippet(07)
snippet(08)
snippet(09)
snippet(10)
snippet(11)
snippet(12)
snippet(13)
snippet(14)
snippet(15)
snippet(16)
snippet(17)
snippet(18)
snippet(19)
snippet(20)
snippet(21)
