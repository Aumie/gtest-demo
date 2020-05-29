cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

project(gtest-demo CXX)

# place binaries and libraries according to GNU standards
include(GNUInstallDirs)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_BINDIR})

# we use this to get code coverage
if(CMAKE_CXX_COMPILER_ID MATCHES GNU)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fprofile-arcs -ftest-coverage")
endif()

add_subdirectory(src)

include(cmake/googletest.cmake)
fetch_googletest(
    ${PROJECT_SOURCE_DIR}/cmake
    ${PROJECT_BINARY_DIR}/googletest
    )

enable_testing()
add_subdirectory(test)

#learn below here
set(darget DIRECTORY)
set_property(
        "${darget}"
        PROPERTY FOO
        1
        2
        3
)
get_property(foo_value "${darget}" PROPERTY FOO)
message(STATUS "${foo_value}")
set(mypoo 4 5 6)
set(target GLOBAL)
set_property(
        "${target}" #or just GLOBAL
        PROPERTY POO
        "${mypoo}"
)
get_cmake_property(poo_value POO)
message(STATUS "${poo_value}")
#set project target
set(projtarget DIRECTORY "${PROJECT_SOURCE_DIR}")
set_property(
        ${projtarget}#or DIRECTORY "${PROJECT_SOURCE_DIR}"
        PROPERTY TOO
        "${mypoo}"
)
get_property(too_value ${projtarget} PROPERTY TOO)
message(STATUS "${too_value}")
#func
function(caller arg)
    message(STATUS "Called ${arg}")
endfunction()
caller(lul)
#func params
function(callers f s t)# increase param = delete arg in ARGN
    foreach(arg IN LISTS ARGN) #or ARGV for all arguments
        message(STATUS "Called ${arg}")
    endforeach()
endfunction()
callers( 1 2 3 4 5)
#example1
set(MY_VARIABLE "var")
message(STATUS "The variable is: ${MY_VARIABLE}")
#example2
set(mybool TRUE)
set(a "a")
set(b "b")
set(value 5)
set(mystr moya)
if(NOT a STREQUAL b AND mybool EQUAL value)
    message(TRUE)
elseif(mystr MATCHES "ya$") # end with sth
    message("matches")
else()
    message("else")
endif()

#example3
set(numb 1)
while (numb LESS 3)
    message("${numb}")
    math(EXPR numb "${numb}+1")
endwhile ()
#example4
foreach(item IN ITEMS bo bo ka)
    message(STATUS "${item}")
endforeach()
foreach(idx RANGE 1 4 2) # or idx RANGE 4 but 0 included, start stop step
    message("${idx}")
endforeach()
