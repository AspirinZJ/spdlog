# Copyright(c) 2019 spdlog authors Distributed under the MIT License (http://opensource.org/licenses/MIT)

cmake_minimum_required(VERSION 3.10)
project(spdlog_examples CXX)

if (NOT TARGET spdlog)
    # Stand-alone build
    find_package(spdlog REQUIRED)
endif ()

# ---------------------------------------------------------------------------------------
# Example of using pre-compiled library
# ---------------------------------------------------------------------------------------
set(EXECUTABLE_TARGETS_LIST "")
add_executable(example example.cpp)
list(APPEND EXECUTABLE_TARGETS_LIST example)

add_executable(spdlogExample spdlogExample.cpp)
list(APPEND EXECUTABLE_TARGETS_LIST spdlogExample)

foreach (EXECUTABLE_TARGET IN LISTS EXECUTABLE_TARGETS_LIST)
    target_link_libraries(${EXECUTABLE_TARGET} PRIVATE spdlog::spdlog)
endforeach ()


# ---------------------------------------------------------------------------------------
# Example of using header-only library
# ---------------------------------------------------------------------------------------
if (SPDLOG_BUILD_EXAMPLE_HO)
    set(EXECUTABLE_TARGETS_LIST_HO "")
    add_executable(example_header_only example.cpp)
    list(APPEND EXECUTABLE_TARGETS_LIST_HO example_header_only)

    add_executable(spdlogExample_header_only spdlogExample.cpp)
    list(APPEND EXECUTABLE_TARGETS_LIST_HO spdlogExample_header_only)

    foreach (EXECUTABLE_TARGET_HO IN LISTS EXECUTABLE_TARGETS_LIST_HO)
        target_link_libraries(${EXECUTABLE_TARGET_HO} PRIVATE spdlog::spdlog_header_only)
    endforeach ()

endif ()
