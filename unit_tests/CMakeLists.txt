find_package(GTest CONFIG REQUIRED)

include(GoogleTest)

add_executable(matrix_tests
	src/unittests_matrix.cpp
)
target_link_libraries(matrix_tests
	PRIVATE
		matrixlib
)
target_link_system_libraries(matrix_tests
	PRIVATE
		GTest::gtest_main
		GTest::gmock
)
target_disable_clang_tidy(matrix_tests)

gtest_discover_tests(matrix_tests)

setup_target_for_coverage_lcov(
	NAME generate_html_report
	EXECUTABLE ctest -j ${PROCESSOR_COUNT}
	DEPENDENCIES matrix_tests
	BASE_DIRECTORY "${CMAKE_SOURCE_DIR}/"
	EXCLUDE "unit_tests/src/*"
	LCOV_ARGS "--no-external"
)