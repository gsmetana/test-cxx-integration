set(TEST_DRIVER test_simple)

include_directories ("${PROJECT_SOURCE_DIR}/simpleLib")

add_executable (${TEST_DRIVER} TEST_simple.cxx)

target_link_libraries (${TEST_DRIVER} simpleLib)

add_test( ${TEST_DRIVER} ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${TEST_DRIVER}  )

if (COVERALLS)
	message("Creating coveralls target for sources:")
	set(COVERAGE_SRCS ${LIB_SRC})
	coveralls_setup("${COVERAGE_SRCS}" 
			ON)
endif()

