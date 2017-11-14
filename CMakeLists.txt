cmake_minimum_required(VERSION 3.7.0)

project(project_template);

set(FLAGS "-pedantic -Wall -Wextra -Wshadow -Wnon-virtual-dtor
-Wold-style-cast -Wcast-align -Wunused -Woverloaded-virtual -Wsign-conversion
-Wconversion -Wnull-dereference -Wdouble-promotion -Wformat=2")

set(CMAKE_PREFIX_PATH ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DNOMINMAX -D_USE_MATH_DEFINES")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${FLAGS}")

find_package(Threads)

find_library(ASSIMP_LIB assimp)
find_library(FMT_LIB fmt)
find_library(VULKAN_LIB vulkan)

add_executable(${PROJECT_NAME} ${CMAKE_SOURCE_DIR}/src/main.cpp)

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR}/include)
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR}/src)

target_link_libraries(${PROJECT_NAME} ${CMAKE_THREAD_LIBS_INIT})
target_link_libraries(${PROJECT_NAME} ${FMT_LIB})
target_link_libraries(${PROJECT_NAME} ${ASSIMP_LIB})
target_link_libraries(${PROJECT_NAME} ${VULKAN_LIB})