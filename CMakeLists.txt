# Project definition
cmake_minimum_required(VERSION 3.1)
project(Raytracer VERSION 0.1.0)

# Source files
set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/lib")
file(GLOB_RECURSE SOURCE_FILES "src/*" "src/*.cpp")
set(SOURCES ${SOURCE_FILES} )

# Executable definition and properties
add_executable(${PROJECT_NAME} ${SOURCES})
target_include_directories(${PROJECT_NAME} PUBLIC "${SRC_DIR}")
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 17)

### External dependencies

# glm
find_package(glm REQUIRED)
include_directories(${GLM_INCLUDE_DIRS})
link_directories(${GLM_LIBRARY_DIRS})
add_definitions(${GLM_DEFINITIONS})

# spdlog
find_package(spdlog REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC spdlog::spdlog)

# lodepng
set(LODEPNG_DIR "${LIB_DIR}/lodepng")
add_library("lodepng" ${LODEPNG_DIR}/lodepng.cpp)
target_include_directories("lodepng" PUBLIC "${LODEPNG_DIR}")
target_link_libraries(${PROJECT_NAME} PUBLIC "lodepng")
