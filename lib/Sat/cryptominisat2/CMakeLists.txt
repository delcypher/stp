include_directories(mtl)
add_library(cryptominisat2 OBJECT
    ClauseAllocator.cpp
    ClauseCleaner.cpp
    FailedVarSearcher.cpp
    FindUndef.cpp
    Gaussian.cpp
    Logger.cpp
    MatrixFinder.cpp
    OnlyNonLearntBins.cpp
    PackedRow.cpp
    PartFinder.cpp
    PartHandler.cpp
    RestartTypeChooser.cpp
    Solver.cpp
    StateSaver.cpp
    Subsumer.cpp
    UselessBinRemover.cpp
    VarReplacer.cpp
    XorFinder.cpp
    XorSubsumer.cpp
    time_mem.cpp
    MemoryPool_src/CMemoryPool.cpp
)
