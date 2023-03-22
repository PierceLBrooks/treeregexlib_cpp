cmake_minimum_required(VERSION 3.12.0 FATAL_ERROR)

project("TreeRegexLib")

macro(set_option var default type docstring)
	if(NOT DEFINED ${var})
		set(${var} ${default})
	endif()
	set(${var} ${${var}} CACHE ${type} ${docstring} FORCE)
endmacro()

set_option(CMAKE_BUILD_TYPE Release STRING "Choose the type of build config variant (\"Debug\" or \"Release\")")

include_directories(${CMAKE_CURRENT_LIST_DIR})

set(TREEREGEXLIB_HEADERS )
list(APPEND TREEREGEXLIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/constants.h)
list(APPEND TREEREGEXLIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/graph.h)
list(APPEND TREEREGEXLIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/timeit.h)
list(APPEND TREEREGEXLIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/transformer.h)
list(APPEND TREEREGEXLIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/tree.h)
list(APPEND TREEREGEXLIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/treeregex_impl.h)
list(APPEND TREEREGEXLIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/treeregex_matching.h)
list(APPEND TREEREGEXLIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/treeregex_to_nfa.h)
install(FILES ${TREEREGEXLIB_HEADERS} DESTINATION ${CMAKE_INSTALL_PREFIX}/include)

set(TREPLACE_SOURCES )
list(APPEND TREPLACE_SOURCES ${CMAKE_CURRENT_LIST_DIR}/treplace.cpp)
list(APPEND TREPLACE_SOURCES ${TREEREGEXLIB_HEADERS})
add_executable(treplace ${TREPLACE_SOURCES})
target_compile_features(treplace PRIVATE cxx_std_14)
install(TARGETS treplace)

set(TSEARCH_SOURCES )
list(APPEND TSEARCH_SOURCES ${CMAKE_CURRENT_LIST_DIR}/tsearch.cpp)
list(APPEND TSEARCH_SOURCES ${TREEREGEXLIB_HEADERS})
add_executable(tsearch ${TSEARCH_SOURCES})
target_compile_features(tsearch PRIVATE cxx_std_14)
install(TARGETS tsearch)

set(TSTRIP_SOURCES )
list(APPEND TSTRIP_SOURCES ${CMAKE_CURRENT_LIST_DIR}/tstrip.cpp)
list(APPEND TSTRIP_SOURCES ${TREEREGEXLIB_HEADERS})
add_executable(tstrip ${TSTRIP_SOURCES})
target_compile_features(tstrip PRIVATE cxx_std_14)
install(TARGETS tstrip)

