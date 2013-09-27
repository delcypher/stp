add_subdirectory(cryptominisat2)

include_directories(cryptominisat2/mtl)

include(MergeStaticLibraries)

add_library(minisat2
    simp/SimpSolver.cc
    core/Solver.cc
    core_prop/Solver_prop.cc
#    utils/Options.cc
    utils/System.cc
)

add_library(sat
    CryptoMinisat.cpp
    MinisatCore.cpp
    MinisatCore_prop.cpp
    SimplifyingMinisat.cpp
)

set(sat_libs cryptominisat2 minisat2)
set(sat_libs_paths "")
foreach(lib ${sat_libs})
    get_property(path_to_lib TARGET ${lib} PROPERTY LOCATION)
    message(STATUS "Got ${path_to_lib} for lib \"${lib}\" ")
    list(APPEND sat_libs_paths ${path_to_lib})
endforeach()
MERGE_STATIC_LIBRARIES(sat ALL "${sat_libs_paths}")
#target_link_libraries(sat
#     core/lib_release.a
#     core_prop/lib_release.a
#     simp/lib_release.a
#     utils/lib_release.a
#    cryptominisat2
#    minisat2
#)
#add_dependencies(simplifier ASTKind_header)
