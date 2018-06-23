#################################################
# cmake file for building DQMNet package
# @author Ete Remi
# Copyright (c)
cmake_minimum_required( VERSION 2.6 FATAL_ERROR )
#################################################

###############################
# project name
project( DQMNet )

set( ${PROJECT_NAME}_VERSION_MAJOR 1 )
set( ${PROJECT_NAME}_VERSION_MINOR 0 )
set( ${PROJECT_NAME}_VERSION_PATCH 0 )

###############################
# Central settings
include( dqm4hep_settings )

# ----- Find Threads for multithreading -----
find_package( Threads REQUIRED )

# ----- Find DQMCore package -----
dqm4hep_find_packages(
  PACKAGES DQMCore
  REQUIRED ADD_DEPENDS
)

# ----- Install doc -----
dqm4hep_build_doxygen()

###############################
# Add source directory
add_subdirectory( source )

###############################
# display some variables and write them to cache
display_std_variables()

###############################
# generate and install following configuration files
dqm4hep_generate_package_configuration(
  PACKAGE_NAME ${PROJECT_NAME}
  LIBRARIES ${PROJECT_NAME} dim
)
