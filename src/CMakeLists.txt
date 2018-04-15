file(GLOB tbb_srcs
        RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
        tbb/*.cpp
        rml/client/rml_tbb.cpp)
file(GLOB tbb_old_srcs
        RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
        old/*.cpp)
list(FILTER tbb_old_srcs EXCLUDE REGEX
        ^old/test_.*\\.cpp$)

file(GLOB tbbmalloc_srcs
        RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
        tbbmalloc/*.cpp
        tbb/itt_notify.cpp)

file(GLOB tbbmalloc_proxy_srcs
        RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
        tbbmalloc/proxy.cpp
        tbbmalloc/tbb_function_replacement.cpp)

list(REMOVE_ITEM tbbmalloc_srcs ${tbbmalloc_proxy_srcs})

if (${CMAKE_SYSTEM_NAME} EQUAL "Linux")
    set(link_libs dl pthread rt)
elseif(${CMAKE_SYSTEM_NAME} EQUAL "Darwin")
    set(link_libs dl pthread)
endif ()

message(STATUS "tbb_srcs: ${tbb_srcs} ${tbb_old_srcs}")
message(STATUS "tbbmalloc_srcs: ${tbbmalloc_srcs}")
message(STATUS "tbbmalloc_proxy_srcs: ${tbbmalloc_proxy_srcs}")

add_library(tbb ${tbb_srcs} ${tbb_old_srcs})
target_compile_definitions(tbb PRIVATE -D__TBB_BUILD=1)
target_include_directories(tbb PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/rml/include
        ${CMAKE_BINARY_DIR})
target_link_libraries(tbb ${link_libs})

add_library(tbbmalloc ${tbbmalloc_srcs})
target_compile_definitions(tbbmalloc PRIVATE -D__TBBMALLOC_BUILD=1)
target_include_directories(tbbmalloc PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_BINARY_DIR})
target_link_libraries(tbbmalloc ${link_libs})

add_library(tbbmalloc_proxy ${tbbmalloc_proxy_srcs})
add_dependencies(tbbmalloc_proxy tbbmalloc)
target_compile_definitions(tbbmalloc_proxy PRIVATE -D__TBBMALLOC_BUILD=1)
target_include_directories(tbbmalloc_proxy PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(tbbmalloc_proxy tbbmalloc ${link_libs})
