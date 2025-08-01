cmake_minimum_required(VERSION 3.10)
project(OpenCRG)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# OpenCRG source files
file(GLOB opencrg_sources
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgMgr.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgMsg.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgStatistics.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgContactPoint.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgEvalxy2uv.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgEvaluv2xy.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgEvalz.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgEvalpk.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgLoader.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgOptionMgmt.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/crgPortability.c
)

# Create static library
add_library(OpenCRG STATIC ${opencrg_sources})

#add_library(OpenCRG::OpenCRG ALIAS OpenCRG)

# Include directories
target_include_directories(OpenCRG PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc>
    $<BUILD_INTERFACE:${OpenCRG_BINARY_DIR}>

)

# Installation rules
set(CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_SOURCE_DIR}/lib)
install(TARGETS OpenCRG 
	ARCHIVE DESTINATION lib
	LIBRARY DESTINATION lib
	COMPONENT library)

#file(GLOB INCLUDES inc/*.h)
#install(FILES ${INCLUDES} DESTINATION include)
