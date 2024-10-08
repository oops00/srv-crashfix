cmake_minimum_required(VERSION 2.8...3.15)
project(scf LANGUAGES C CXX)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})

set(SUBHOOK_FORCE_32BIT BOOL ON)
set(SUBHOOK_STATIC      BOOL ON)
set(SUBHOOK_TESTS       BOOL OFF)
add_subdirectory(libraries/subhook)

include_directories(includes libraries/urmem)
add_library(${PROJECT_NAME} MODULE)
target_sources(${PROJECT_NAME} PRIVATE source/main.cpp source/main.def)
target_link_libraries(${PROJECT_NAME} subhook)

if(CMAKE_COMPILER_IS_GNUCC)
    set_target_properties(${PROJECT_NAME} PROPERTIES COMPILE_FLAGS "-m32 -c -O3 -w" LINK_FLAGS "-m32 -O3 -static-libgcc -static-libstdc++")
endif()