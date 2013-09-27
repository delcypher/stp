include_directories(${CMAKE_CURRENT_BINARY_DIR}/../AST/)

configure_file("${CMAKE_CURRENT_SOURCE_DIR}/GitSHA1.cpp.in" "${CMAKE_CURRENT_BINARY_DIR}/GitSHA1.cpp" @ONLY)

add_library(stp-lib
    Globals.cpp
    ${CMAKE_CURRENT_BINARY_DIR}/GitSHA1.cpp
    $<TARGET_OBJECTS:stpmgr>
    $<TARGET_OBJECTS:AST>
    $<TARGET_OBJECTS:abstractionrefinement>
    $<TARGET_OBJECTS:tosat>
    $<TARGET_OBJECTS:printer>
    $<TARGET_OBJECTS:sat>
    $<TARGET_OBJECTS:cryptominisat2>
    $<TARGET_OBJECTS:minisat2>
    $<TARGET_OBJECTS:simplifier>
    $<TARGET_OBJECTS:constantbv>
    $<TARGET_OBJECTS:abc>
    $<TARGET_OBJECTS:cinterface>
    $<TARGET_OBJECTS:parser>
    ${Boost_LIBRARIES}
)

message(STATUS Boost ${Boost_LIBRARIES})

set_target_properties(stp-lib PROPERTIES OUTPUT_NAME stp)
set_target_properties(stp-lib PROPERTIES ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
target_link_libraries(stp-lib cppinterface)

add_executable(stp
    main.cpp
)
set_target_properties(stp PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
target_link_libraries(stp
    stp-lib
)
