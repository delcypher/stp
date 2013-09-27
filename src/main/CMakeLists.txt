include_directories(${CMAKE_CURRENT_BINARY_DIR}/../AST/)

configure_file("${CMAKE_CURRENT_SOURCE_DIR}/GitSHA1.cpp.in" "${CMAKE_CURRENT_BINARY_DIR}/GitSHA1.cpp" @ONLY)

add_library(stp-lib
    Globals.cpp
    ${CMAKE_CURRENT_BINARY_DIR}/GitSHA1.cpp
)
set_target_properties(stp-lib PROPERTIES OUTPUT_NAME stp)
set_target_properties(stp-lib PROPERTIES ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})

include(MergeStaticLibraries)

set(stp_libs
    AST
    stpmgr
    abstractionrefinement
    tosat
    sat
    simplifier
    constantbv
    abc
    cinterface
    parser
    printer
)

set(stp_libs_paths "")
foreach(lib ${stp_libs})
    get_property(path_to_lib TARGET ${lib} PROPERTY LOCATION)
    message(STATUS "Got ${path_to_lib} for lib \"${lib}\" ")
    list(APPEND stp_libs_paths ${path_to_lib})
endforeach()

message(STATUS "Using ${stp_libs_paths}")
MERGE_STATIC_LIBRARIES(stp-lib ALL "${stp_libs_paths}")

add_executable(stp
    main.cpp
)
set_target_properties(stp PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
target_link_libraries(stp
    stp-lib
)
