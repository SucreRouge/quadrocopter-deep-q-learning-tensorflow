cmake_minimum_required (VERSION 2.8.1)
set(CMAKE_CXX_STANDARD 11)

add_definitions(-DTF_GRAPH_DIR=${TF_GRAPH_DIR} -DTF_GRAPH_SAVE_DIR=${TF_GRAPH_SAVE_DIR})

include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
        message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

SET_PROPERTY(GLOBAL PROPERTY TARGET_SUPPORTS_SHARED_LIBS TRUE)
cmake_policy(SET CMP0015 NEW) #for relative paths in link_directories

add_subdirectory(Quadrocopter-Box2D/Quadrocopter-Box2D/Quadrocopter-Box2D)
add_subdirectory(Quadrocopter2DBrain/Quadrocopter2DBrain)
add_subdirectory(Quadrocopter-Visualizer/Classes)

include_directories(
Quadrocopter-Box2D/Quadrocopter-Box2D/Quadrocopter-Box2D
Quadrocopter2DBrain/Quadrocopter2DBrain
Quadrocopter-Visualizer/Classes
)
