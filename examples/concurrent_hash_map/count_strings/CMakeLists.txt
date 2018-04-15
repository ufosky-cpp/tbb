add_executable(count_strings count_strings.cpp)
add_dependencies(count_strings tbb)
target_link_libraries(count_strings tbb)
