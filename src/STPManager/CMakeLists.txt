include_directories(${CMAKE_CURRENT_BINARY_DIR}/../AST/)
add_library(stpmgr OBJECT
    STP.cpp
    STPManager.cpp
)

#Eurgh
#target_link_libraries(stpmgr
#    AST
#)
