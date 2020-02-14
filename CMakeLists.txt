cmake_minimum_required(VERSION 3.15)
project(test)

find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)
include_directories(${OPENGL_INCLUDE_DIR})
include_directories(${GLUT_INCLUDE_DIR})

set(CMAKE_CXX_STANDARD 14)

add_executable(test main.cpp glad.c)
add_executable(1.1 HelloTriangle/HelloTriangle_1.cpp glad.c)
add_executable(1.2 HelloTriangle/HelloTriangle_2.cpp glad.c)


# specify the search location
set( _glfw3_HEADER_SEARCH_DIRS "/usr/local/include")
set( _glfw3_LIB_SEARCH_DIRS "/usr/local/lib")

set( _glfw3_ENV_ROOT $ENV{GLFW3_ROOT} )
if( NOT GLFW3_ROOT AND _glfw3_ENV_ROOT )
    set(GLFW3_ROOT ${_glfw3_ENV_ROOT} )
endif()

# Put user specified location at beginning of search
if( GLFW3_ROOT )
    list( INSERT _glfw3_HEADER_SEARCH_DIRS 0 "${GLFW3_ROOT}/include" )
    list( INSERT _glfw3_LIB_SEARCH_DIRS 0 "${GLFW3_ROOT}/lib" )
endif()

# Search for the header
FIND_PATH(GLFW3_INCLUDE_DIR "GLFW/glfw3.h" PATHS ${_glfw3_HEADER_SEARCH_DIRS})

# Search for the library
FIND_LIBRARY(GLFW3_LIBRARY NAMES libglfw.3.4.dylib PATHS ${_glfw3_LIB_SEARCH_DIRS} )

#include header file directory
include_directories(${GLFW3_INCLUDE_DIR})

#include library file directory
link_directories(${_glfw3_LIB_SEARCH_DIRS})

#link library file
target_link_libraries(test ${GLFW3_LIBRARY})
target_link_libraries(1.1 ${GLFW3_LIBRARY})
target_link_libraries(1.2 ${GLFW3_LIBRARY})


# include all header file directories
link_libraries(1.1 ${GLFW3_INCLUDE_DIR} ${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIRS})
link_libraries(1.2 ${GLFW3_INCLUDE_DIR} ${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIRS})
link_libraries(test ${GLFW3_INCLUDE_DIR} ${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIRS})