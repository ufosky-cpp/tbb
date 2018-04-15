set(src_dir ${CMAKE_CURRENT_SOURCE_DIR})

file(GLOB_RECURSE srcs
        RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}"
        "${src_dir}/*.cpp")
add_executable(sub_string_finder sub_string_finder.cpp)
add_dependencies(sub_string_finder tbb)
target_link_libraries(sub_string_finder tbb)
