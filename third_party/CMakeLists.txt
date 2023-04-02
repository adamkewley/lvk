cmake_minimum_required(VERSION 3.10)

project(learn-vulkan-deps)

include(ExternalProject)  # ExternalProject_Add
include(GNUInstallDirs)  # CMAKE_INSTALL_LIBDIR

# setup `LVK_DEPENDENCY_CMAKE_ARGS`
#
# these are cache args that should be forwarded to external dependency projects
if(TRUE)
    set(LVK_FORWARDED_ARGS

        CMAKE_CXX_COMPILER
        CMAKE_C_COMPILER
        CMAKE_CXX_FLAGS
        CMAKE_CXX_FLAGS_DEBUG
        CMAKE_CXX_FLAGS_MINSIZEREL
        CMAKE_CXX_FLAGS_RELEASE
        CMAKE_CXX_FLAGS_RELWITHDEBINFO
        CMAKE_C_FLAGS
        CMAKE_C_FLAGS_DEBUG
        CMAKE_C_FLAGS_MINSIZEREL
        CMAKE_C_FLAGS_RELEASE
        CMAKE_C_FLAGS_RELWITHDEBINFO
        CMAKE_BUILD_TYPE
        CMAKE_INSTALL_PREFIX
    )
    foreach(LVK_FORWARDED_ARG IN LISTS LVK_FORWARDED_ARGS)
        list(APPEND LVK_DEPENDENCY_CMAKE_ARGS -D${LVK_FORWARDED_ARG}:STRING=${${LVK_FORWARDED_ARG}})
    endforeach()
    unset(LVK_FORWARDED_ARGS)
endif()

ExternalProject_Add(glm
    SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/glm
    CMAKE_CACHE_ARGS
        ${LVK_DEPENDENCY_CMAKE_ARGS}
        -DBUILD_TESTING:BOOL=OFF
)
