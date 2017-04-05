cmake_minimum_required( VERSION 3.6.2 )
project(PokerStove)

include(DownloadProject.cmake)

set(UPDATE_DISCONNECTED_IF_AVAILABLE "UPDATE_DISCONNECTED 1")

include(DownloadProject.cmake)
download_project(PROJ                googletest
    GIT_REPOSITORY      https://github.com/google/googletest.git
    GIT_TAG             master
    ${UPDATE_DISCONNECTED_IF_AVAILABLE}
    )

# Prevent GoogleTest from overriding our compiler/linker options
# when building with Visual Studio
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

download_project(PROJ fmt
    GIT_REPOSITORY https://github.com/fmtlib/fmt.git
    GIT_TAG master
    ${UPDATE_DISCONNECTED_IF_AVAILABLE}
    )

download_project(PROJ cppext
    GIT_REPOSITORY https://github.com/horttanainen/cppext.git
    GIT_TAG master
    ${UPDATE_DISCONNECTED_IF_AVAILABLE}
    )

add_subdirectory(
    ${googletest_SOURCE_DIR}
    ${googletest_BINARY_DIR}
    )

add_subdirectory(
    ${fmt_SOURCE_DIR}
    ${fmt_BINARY_DIR}
    )

add_subdirectory(
    ${cppext_SOURCE_DIR}
    ${cppext_BINARY_DIR}
    )

add_subdirectory(src)