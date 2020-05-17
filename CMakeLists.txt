cmake_minimum_required(VERSION 3.10)

project(HelloProject)

add_executable(hello main.cpp)

install(TARGETS hello RUNTIME DESTINATION bin)

enable_testing()
add_test(NAME hello COMMAND hello)

###cpack
string(TIMESTAMP vTimeStamp "%Y%m%d%H%M%S")
execute_process(
    COMMAND git log -1 --format=%h
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    OUTPUT_VARIABLE vGitCommit
    OUTPUT_STRIP_TRAILING_WHITESPACE
)
execute_process(
    COMMAND git rev-parse --abbrev-ref HEAD
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    OUTPUT_VARIABLE vGitBranch
    OUTPUT_STRIP_TRAILING_WHITESPACE
)

set(CPACK_GENERATOR "TGZ")
set(CPACK_PACKAGE_FILE_NAME "${PROJECT_NAME}-${vTimeStamp}-${vGitBranch}-${vGitCommit}")
include(CPack)
