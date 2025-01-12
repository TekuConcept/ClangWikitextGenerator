CMAKE_MINIMUM_REQUIRED(VERSION 3.16.0)
PROJECT(clang-parser)

SET(CMAKE_CXX_STANDARD 17)
SET(CMAKE_CXX_STANDARD_REQUIRED YES)
SET(CMAKE_CXX_EXTENSIONS NO)

FIND_PACKAGE(Clang REQUIRED)
SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${LLVM_CMAKE_DIR}")
INCLUDE(AddLLVM)

INCLUDE_DIRECTORIES(
    ${CMAKE_SOURCE_DIR}/Include
    ${LLVM_INCLUDE_DIRS}
    ${CLANG_INCLUDE_DIRS}
)

ADD_DEFINITIONS(
    ${LLVM_DEFINITIONS}
    ${CLANG_DEFINITIONS}
)

FILE(GLOB_RECURSE AWESOME_SAUCE ${CMAKE_SOURCE_DIR}/Source/*.cpp)
ADD_LLVM_LIBRARY(wiki-generator MODULE
    ${AWESOME_SAUCE}
    PLUGIN_TOOL clang
)
