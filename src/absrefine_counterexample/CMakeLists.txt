include_directories(${CMAKE_CURRENT_BINARY_DIR}/../AST/)
add_library(abstractionrefinement OBJECT
    AbstractionRefinement.cpp
    CounterExample.cpp
)
add_dependencies(abstractionrefinement ASTKind_header)
