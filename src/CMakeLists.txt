add_executable(checker Checker.cpp
  Verifier.cpp)
target_include_directories(checker PUBLIC ${local_include})

if (LLVM_FOUND)
  add_library(InputGen MODULE
    InputGen.cpp)

  target_include_directories(InputGen PUBLIC ${local_include} ${LLVM_INCLUDE_DIRS})
  llvm_map_components_to_libnames(llvm_libs support core analysis)
  #  target_link_libraries(InputGen PRIVATE ${llvm_libs})
  set_target_properties(InputGen PROPERTIES
    COMPILE_FLAGS "-fno-rtti")
endif()

add_executable(score_calc score_calc.cpp)
