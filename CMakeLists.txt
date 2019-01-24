cmake_minimum_required(VERSION 2.6)
project(riscv-disassembler)

set(SOURCE_FILES
    src/riscv-disas.c
    )

# target
add_library(riscv-disassembler STATIC ${SOURCE_FILES})

#target_compile_options(riscv-disassembler PRIVATE -std=gnu99)

target_compile_options(riscv-disassembler PRIVATE -O2)
target_compile_options(riscv-disassembler PRIVATE -fdiagnostics-show-option)
target_include_directories( riscv-disassembler PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)

if (BUILD_TESTS)
    # test-disas execautable
    project(test-disas)
    add_executable(test-disas src/test-disas.c)
    target_link_libraries(test-disas riscv-disassembler)

    # test-encode execautable
    project(test-encode)
    add_executable(test-encode src/test-disas.c)
    target_link_libraries(test-encode riscv-disassembler)
endif(BUILD_TESTS)

