cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)
set(EXE_NAME graphicsDemo)

if(NOT DEFINED CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE RelWithDebInfo CACHE STRING "Build type")
endif()

project(demos CXX)
set(CMAKE_CXX_STANDARD 14)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

set(WINDOW_DEMO_LIBRARIES "")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

find_package(SFML REQUIRED COMPONENTS network system graphics audio window)
include_directories(${SFML_INCLUDE_DIR})
list(APPEND WINDOW_DEMO_LIBRARIES ${SFML_LIBRARIES})

find_package(Catch REQUIRED)
list(APPEND WINDOW_DEMO_LIBRARIES ${CATCH_INCLUDE_DIR})

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

if (${CMAKE_CXX_COMPILER_ID} STREQUAL "GNU")
  add_definitions("-Wall")
endif ()

add_subdirectory(source)

#### UNIT TESTING ####

include_directories(${WINDOW_DEMO_LIBRARIES})
enable_testing()
add_subdirectory(tests)

if (CMAKE_VERSION VERSION_GREATER 2.8.5)
  include(FeatureSummary)
  feature_summary(WHAT ALL)
endif ()
