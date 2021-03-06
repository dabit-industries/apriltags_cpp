# swatbotics/apriltags-cpp/CMakeLists.txt

cmake_minimum_required(VERSION 2.6)

project(APRILTAGS)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

if(APPLE)
  include_directories(/opt/local/include) # MacPorts
  link_directories(/opt/local/lib)
  find_library(OPENGL_LIBRARY OpenGL)
else()
  find_library(OPENGL_LIBRARY GL)
  find_library(GLU_LIBRARY GLU)
  set(OPENGL_LIBRARY ${OPENGL_LIBRARY} ${GLU_LIBRARY})
endif()

find_library(GLUT_LIBRARY glut)
find_package(OpenCV 2.3.1)

include(FindPkgConfig)

include_directories(${OpenCV_INCLUDE_DIRS})

pkg_check_modules(CAIRO cairo)

if (${CAIRO_FOUND})
add_definitions(-DMZ_HAVE_CAIRO)
endif ()

find_package( CGAL QUIET COMPONENTS  )

if (CGAL_FOUND)
  include( ${CGAL_USE_FILE} )
  add_definitions(-DHAVE_CGAL)
  find_package( Boost REQUIRED )
else()
  message("CGAL not found, can not use new quad detector")
endif()

set(CMAKE_C_FLAGS "-Wall -g")
set(CMAKE_CXX_FLAGS "-Wall -g")

if (APPLE OR UNIX)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wsign-compare -frounding-math")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wsign-compare -frounding-math")
endif()

set(CMAKE_C_FLAGS_DEBUG "-O")
set(CMAKE_CXX_FLAGS_DEBUG "-O")

set(CMAKE_C_FLAGS_RELEASE "-O2")
set(CMAKE_CXX_FLAGS_RELEASE "-O2")

add_subdirectory(src)

install(DIRECTORY src/ DESTINATION include/apriltags_cpp FILES_MATCHING PATTERN "*.h" PATTERN ".svn" EXCLUDE)
install(FILES package.xml DESTINATION share/apriltags_cpp)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/cmake/Config.cmake.in "${PROJECT_BINARY_DIR}/apriltags_cppConfig.cmake" @ONLY)
install(FILES "${PROJECT_BINARY_DIR}/apriltags_cppConfig.cmake" DESTINATION share/apriltags_cpp/cmake)
