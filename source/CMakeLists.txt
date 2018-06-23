#######################################################
# cmake file for building DQMNet package
# @author Ete Remi
# Copyright (c) 
#######################################################

add_subdirectory( dim )

# include directories
include_directories( SYSTEM dim/include )
include_directories( SYSTEM asio )
include_directories( SYSTEM websocketpp )
include_directories( BEFORE include )
add_definitions( -DASIO_STANDALONE )
dqm4hep_set_cxx_flags()

# -------------------------------------------------
# build the project library
aux_source_directory( src SRC_FILES )
add_shared_library( ${PROJECT_NAME} ${SRC_FILES} )
target_link_libraries( ${PROJECT_NAME} dim_shared )
install( TARGETS ${PROJECT_NAME} LIBRARY DESTINATION lib )

# -------------------------------------------------
# main executable
dqm4hep_add_main_executables( EXCEPT dqm4hep-ws-server )

# -------------------------------------------------
# clang tidy and format rules
dqm4hep_run_clang_tidy()
dqm4hep_run_clang_format()

install_directory( include DESTINATION . FILES_MATCHING PATTERN "*.h" )
