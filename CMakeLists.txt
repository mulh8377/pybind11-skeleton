cmake_minimum_required(VERSION 3.0.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_FLAGS "-O3")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")

project (pyskeleton)

include_directories("${CMAKE_SOURCE_DIR}/include")
include_directories("${CMAKE_SOURCE_DIR}/src")
include_directories("${CMAKE_SOURCE_DIR}/python")
add_subdirectory("${CMAKE_SOURCE_DIR}/pybind11")

file (GLOB SOURCE_FILES "src/*.cpp")
file (GLOB HEADER_FILES "include/*.hpp")
file (GLOB PYTHON_FILES "python/*.cpp" "python/*.hpp")

pybind11_add_module(pyskeleton
	${SOURCE_FILES}
	${HEADER_FILES}
	${PYTHON_FILES}
)

target_link_libraries(pyskeleton PUBLIC)

install(TARGETS pyskeleton
  COMPONENT python
  LIBRARY DESTINATION "usr/lib"
  )