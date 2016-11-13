cmake_minimum_required(VERSION 2.8)

# a simple test case
project (Simple)


set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} 
    ${PROJECT_SOURCE_DIR}/coveralls-cmake/cmake)


option(COVERALLS "Generate coveralls data" OFF)


option(WITH_TEST_PROGRAMS "Turns on compilation of tester programs" ON)
option(WITH_UNIT_TESTS "Turn on compilation of unit test" ON)

# Turn on coverage if we're running coveralls!
if (COVERALLS)
   include(Coveralls)

   # This adds coverage arguments to gcc/clang.
   coveralls_turn_on_coverage()
endif()

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_HOME_DIRECTORY}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_HOME_DIRECTORY}/bin)

set(LIB_SRC
  "${PROJECT_SOURCE_DIR}/simpleLib/simpleLib.cxx" 
  "${PROJECT_SOURCE_DIR}/simpleLib/simpleCLib.c" 
  "${PROJECT_SOURCE_DIR}/simpleLib/simpleWe.cpp")

set(LIB_HDR "")

add_library(simpleLib STATIC ${LIB_SRC} ${LIB_HDR})


if (WITH_UNIT_TESTS)

	ENABLE_TESTING()
	add_subdirectory(test)
endif()
