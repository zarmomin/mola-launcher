# ------------------------------------------------------------------------------
#        A Modular Optimization framework for Localization and mApping
#                               (MOLA)
#
# Copyright (C) 2018-2019, Jose Luis Blanco-Claraco, contributors (AUTHORS.md)
# All rights reserved.
# Released under GNU GPL v3. See LICENSE file
# ------------------------------------------------------------------------------

find_package(mrpt-core)
find_package(mrpt-tclap) # tclap wrapper, useful for Windows, etc.

FIND_PACKAGE(PkgConfig REQUIRED)

find_package(yaml_cpp_catkin QUIET)
if(${yaml_cpp_catkin_FOUND})
  message(STATUS "Found yaml_cpp_catkin, using instead of system library.")
  set(YamlCpp_LIBRARIES ${yaml_cpp_catkin_LIBRARIES})
  set(YamlCpp_INCLUDE_DIRS ${yaml_cpp_catkin_INCLUDE_DIRS})
else()
  message(STATUS "No yaml_cpp_catkin, using yaml-cpp system library instead.")
  pkg_check_modules(YamlCpp REQUIRED yaml-cpp>=0.5)
endif()

mola_add_executable(
	TARGET  mola-cli
	SOURCES mola-cli.cpp
	LINK_LIBRARIES
		mola-launcher
		mrpt::core
		mrpt::tclap
		yaml-cpp
)

mola_add_executable(
	TARGET  mola-dir
	SOURCES mola-dir.cpp
	LINK_LIBRARIES
		mola-launcher
)
