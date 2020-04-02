#-------------------------------------------------------------------------------
#	CMAKE SETTINGS
#-------------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.12.0)
#-------------------------------------------------------------------------------
#	SOURCE CODE
#-------------------------------------------------------------------------------
file(GLOB_RECURSE HEADER_FILES "src/*.h")
file(GLOB_RECURSE SOURCE_FILES "src/*.cpp")
#-------------------------------------------------------------------------------
#	PROJECT SETTINGS
#-------------------------------------------------------------------------------
set(TARGET_NAME glfw-examples)
set(PROJECT_NAME ${TARGET_NAME})
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
project(${PROJECT_NAME} LANGUAGES CXX)
#-------------------------------------------------------------------------------
#	GLFW SETTINGS
#-------------------------------------------------------------------------------
find_package(OpenGL REQUIRED)

set(GLFWPath ${PROJECT_SOURCE_DIR}/glfw)
set(GLEWPath ${PROJECT_SOURCE_DIR}/glew)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory(${GLFWPath})
add_subdirectory(${GLEWPath}/build/cmake)
#-------------------------------------------------------------------------------
#	ADDITIONAL LIBRARIES
#-------------------------------------------------------------------------------
list(APPEND LIBRARIES
OpenGL::GL
glfw
glew_s
)
#-------------------------------------------------------------------------------
#	GENERATE EXECUTABLE
#-------------------------------------------------------------------------------
# Generate the executable
add_executable(${TARGET_NAME} ${HEADER_FILES} ${SOURCE_FILES})
# link include directories
target_include_directories(${TARGET_NAME} PRIVATE
    ${GLFWPath}/include
    ${GLEWPath}/include
)
# link libraries
target_link_libraries(${TARGET_NAME} ${LIBRARIES} ${GLFW_LIBRARIES})
