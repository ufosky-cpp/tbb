add_executable(Fibonacci Fibonacci.cpp)
add_dependencies(Fibonacci tbb)
target_link_libraries(Fibonacci tbb)
