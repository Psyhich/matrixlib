find_package(fmt CONFIG REQUIRED)

add_library(matrixlib
	src/matrixes.cpp
)
target_link_libraries(matrixlib
	PUBLIC
		fmt::fmt
	PRIVATE
		project_options
		project_warnings
)
target_include_directories(matrixlib 
	PRIVATE
		include
		"${CMAKE_BINARY_DIR}/configured_files/include"
)
target_include_interface_directories(matrixlib
	include
)
set_target_properties(matrixlib
	PROPERTIES
		OUTPUT_NAME "matrix"
)
