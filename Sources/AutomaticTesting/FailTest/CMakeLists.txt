#-------------------------------------
# Currently used CMake Version
#-------------------------------------
cmake_minimum_required(VERSION 3.0)

#-------------------------------------
# Subdirectories (please add in alphabetical Order)
#-------------------------------------
MACRO(SUBDIRLIST result curdir)
  FILE(GLOB children RELATIVE ${curdir} ${curdir}/*)
  SET(dirlist "")
  FOREACH(child ${children})
    IF(IS_DIRECTORY ${curdir}/${child})
    LIST(APPEND dirlist ${child})
    ENDIF()
  ENDFOREACH()
  SET(${result} ${dirlist})
ENDMACRO()

SUBDIRLIST(SUBDIRS ${CMAKE_CURRENT_SOURCE_DIR})

FOREACH(subdir ${SUBDIRS})
    ADD_SUBDIRECTORY(${subdir})
ENDFOREACH()

#-------------------------------------
# Get Compiler Paths
#-------------------------------------
INCLUDE(${CMAKE_CURRENT_SOURCE_DIR}/../../OpenppConfig.txt)

#-------------------------------------
# Information about the Project
#-------------------------------------
string(REPLACE ${BASE_PATH} "" ProjectName ${CMAKE_CURRENT_SOURCE_DIR})
string(REPLACE "/" "" ProjectName ${ProjectName})
string(REPLACE ":" "" ProjectName ${ProjectName})
string(REPLACE "." "" ProjectName ${ProjectName})
string(REPLACE "_" "" ProjectName ${ProjectName})
project(${ProjectName})

#-------------------------------------
# Sources and Headers
#-------------------------------------
SET(${PROJECT_NAME}_SOURCES

    main.cpp
)
SET(${PROJECT_NAME}_HEADERS

)

#-------------------------------------
# Create Binary
#-------------------------------------
add_executable(${PROJECT_NAME} ${${PROJECT_NAME}_SOURCES} ${${PROJECT_NAME}_HEADERS})

#-------------------------------------
# Configure install
#-------------------------------------
install(TARGETS ${PROJECT_NAME}
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib/static)
