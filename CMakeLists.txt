cmake_minimum_required( VERSION 3.6.2 )
project(PokerStove)

include(DownloadProject.cmake)

set(UPDATE_DISCONNECTED_IF_AVAILABLE "UPDATE_DISCONNECTED 1")

if(dev_build)
    include(DownloadProject.cmake)
    download_project(PROJ                googletest
        GIT_REPOSITORY      https://github.com/google/googletest.git
        GIT_TAG             master
        ${UPDATE_DISCONNECTED_IF_AVAILABLE}
        )

    # Prevent GoogleTest from overriding our compiler/linker options
    # when building with Visual Studio
    set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
endif(dev_build)

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

download_project(PROJ boost-binomial
    GIT_REPOSITORY https://github.com/horttanainen/boost-binomial.git
    GIT_TAG master
    ${UPDATE_DISCONNECTED_IF_AVAILABLE}
    )

if(dev_build)
    add_subdirectory(
        ${googletest_SOURCE_DIR}
        ${googletest_BINARY_DIR}
        )
endif()

add_subdirectory(
    ${fmt_SOURCE_DIR}
    ${fmt_BINARY_DIR}
    )

add_subdirectory(
    ${boost-binomial_SOURCE_DIR}
    ${boost-binomial_BINARY_DIR}
    )

add_subdirectory(
    ${cppext_SOURCE_DIR}
    ${cppext_BINARY_DIR}
    )

add_subdirectory(src)
