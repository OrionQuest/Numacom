# Basic Project Information
cmake_minimum_required(VERSION 3.0)
set (CMAKE_CXX_STANDARD 11)
project(CS323)

# Add the cmake/Modules directory for external dependency location scripts
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")
INCLUDE(FindPkgConfig)

# add a target to generate API documentation with Doxygen/Sphinx
find_package(Sphinx)
if(SPHINX_FOUND)
  add_custom_target(doc
    ${SPHINX_EXECUTABLE} -b html ${CMAKE_CURRENT_SOURCE_DIR}/docs_src ${CMAKE_CURRENT_SOURCE_DIR}/../Numacom_Documentation/html
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    COMMENT "Generating API documentation with Sphinx" VERBATIM
    )
  add_custom_target(prep_doc COMMAND ${CMAKE_COMMAND} -E make_directory ${CMAKE_CURRENT_BINARY_DIR}/docs )
endif(SPHINX_FOUND)
