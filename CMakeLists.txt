cmake_minimum_required(VERSION 3.5)
project(vulkan_sandbox CXX)

#set (CMAKE_CXX_FLAGS "  -v -m64  -O3 -Wno-c++98-compat -Wno-global-constructors -Wno-exit-time-destructors -Wno-padded -Wno-missing-prototypes -Wno-missing-variable-declarations")
set(CMAKE_COLOR_MAKEFILE TRUE)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED YES)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_VERBOSE_MAKEFILE 1)
# Set CMake modules search path
######################################
file(GLOB_RECURSE SOURCE_FILES
        ${CMAKE_SOURCE_DIR}/src/*.c
        ${CMAKE_SOURCE_DIR}/src/*.cpp)

# Add header files
file(GLOB_RECURSE HEADER_FILES
        ${CMAKE_SOURCE_DIR}/src/*.h
        ${CMAKE_SOURCE_DIR}/src/*.hpp)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY  "${CMAKE_CURRENT_SOURCE_DIR}/bin")

find_package(Vulkan REQUIRED)
if(Vulkan_FOUND)
    include_directories(${Vulkan_INCLUDE_DIRS})
    message(STATUS "Found Vulkan lib -- " ${Vulkan_LIBRARY} )
endif()

find_package(glfw3 REQUIRED)
if(glfw3_FOUND)
    include_directories(${GLFW3_INCLUDE_DIRS})
endif()

find_package(glm REQUIRED static)
if(glm_FOUND)
    include_directories(${GLM_INCLUDE_DIRS})
endif()
# Define target name
set (TARGET_NAME vulkan-sanbox)

# Define libs
set(LIBS ${LIBS} ${Vulkan_LIBRARY} glfw glm)
# uncomment to test set up of vulkan and deps
#add_executable(vulkan_sandbox test_vulkan_and_deps.cpp)
add_executable(vulkan_sandbox src/main.cpp src/main.h)
target_link_libraries( vulkan_sandbox  ${LIBS})