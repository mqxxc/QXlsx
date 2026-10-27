# CMake 最低版本限制
cmake_minimum_required (VERSION 3.10)

# 设置项目名称
set(PROJECT_NAME "Qxlsx")

set(CMAKE_DEBUG_POSTFIX "d")
project(${PROJECT_NAME} VERSION 1.5.0.1)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOMOC ON)

FILE (GLOB_RECURSE ALL_SOURCES "./src/*.cpp" "./src/*.c")
FILE (GLOB_RECURSE ALL_INCLUDES "./include/*.hpp" "./include/*.h")


add_library(${PROJECT_NAME} STATIC
    ${ALL_SOURCES}
    ${ALL_INCLUDES}
)

find_package(Qt5 REQUIRED COMPONENTS 
    Core 
    Gui
)

target_include_directories(${PROJECT_NAME} PRIVATE 
    ./include
    ./private
    ${Qt5_INCLUDE_DIR}/QtGui/${Qt5Core_VERSION}/QtGui
    ${Qt5_INCLUDE_DIR}/QtGui/${Qt5Core_VERSION}
    ${Qt5_INCLUDE_DIR}/QtCore/${Qt5Core_VERSION}
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    Qt5::Gui
    Qt5::Core
)