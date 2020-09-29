cmake_minimum_required(VERSION 3.10)

# set the project name
project(FirstOrganizedCMake VERSION 1.0)

# use the CMAKE_CXX_STANDARD variable
set(CMAKE_CXX_STANDARD  11)
set(CMAKE_CXX_STANDARD_REQUIERED TRUE)

#export configuration to source code
configure_file(cmake/FirstOrganizedCMakeConfig.h.in FirstOrganizedCMakeConfig.h)

#about libraries
add_subdirectory(src/log_lib)

#about executable
option(FIRSTORGANIZEDCMAKE_WITH_EXECUTABLES "Compile mains" OFF)
if(FIRSTORGANIZEDCMAKE_WITH_EXECUTABLES)
	#Enable testing with CTest
	message(STATUS "Configuring FirstOrganizedCMake with executables")
	add_subdirectory(mains)
endif()

#about tests
option(FIRSTORGANIZEDCMAKE_WITH_TESTS "Compile testprojects" OFF)
if(FIRSTORGANIZEDCMAKE_WITH_TESTS)
	# Enable testing with CTest
	enable_testing()
	message(STATUS "Configuring FirstOrganizedCMake withtests")
	add_subdirectory(tests)
endif()

include(CMakePackageConfigHelpers) 
# define the following command
configure_package_config_file(
cmake/FirstOrganizedCMakeConfig.cmake.in 
FirstOrganizedCMakeConfig.cmake
INSTALL_DESTINATION ${PROJECT_BINARY_DIR}
)

