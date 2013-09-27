#add_custom_target(ASTKind_header ALL DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/ASTKind.h)
include_directories(${CMAKE_CURRENT_BINARY_DIR}/../AST/)

add_library(cinterface OBJECT
    c_interface.cpp
)

add_dependencies(cinterface ASTKind_header)

# -----------------------------------------------------------------------------
# Copy over public headers
# -----------------------------------------------------------------------------

set(public_headers c_interface.h)

# This is a stupid hack to get
# aroudn the restriction
# that OBJECT targets in CMake
# cannot have custom commands
# that use PRE_BUILD, PRE_LINK
# or POST_BUILD.
add_custom_target(public_headers ALL DEPENDS cinterface)


foreach(public_header ${public_headers})
    add_custom_command(TARGET  public_headers
                       COMMAND ${CMAKE_COMMAND} -E
                           echo Copying public header ${public_header}
                       COMMAND ${CMAKE_COMMAND} -E
                           copy ${CMAKE_CURRENT_SOURCE_DIR}/${public_header}
                                ${CMAKE_BINARY_DIR}/include/stp/${public_header}
                      )
endforeach()
