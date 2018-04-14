cmake_minimum_required(VERSION 3.10)
project(tbb ASM C CXX)

#set(CMAKE_CXX_STANDARD 03)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_FIND_LIBRARY_SUFFIXES ".so" ".dylib" ".dll" ".a" ".dll.a")
set(CMAKE_CPP_FLAGS
        "-DDO_ITT_NOTIFY -DUSE_PTHREAD -D__TBB_BUILD=1"
        )
set(CMAKE_CXX_FLAGS "${CMAKE_CPP_FLAGS} -Wall -fpermissive")
set(CMAKE_C_FLAGS  "${CMAKE_CPP_FLAGS} -Wall")

execute_process(
        COMMAND sh build/version_info_linux.sh
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        OUTPUT_FILE ${CMAKE_CURRENT_BINARY_DIR}/version_string.ver
)

execute_process(
        COMMAND sh build/generate_tbbvars.sh
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)

include_directories(
        include
        src
        src/rml/include
        ${CMAKE_CURRENT_BINARY_DIR}
)
add_library(tbb
        src/tbb/concurrent_hash_map.cpp
        src/tbb/concurrent_queue.cpp
        src/tbb/concurrent_vector.cpp
        src/tbb/dynamic_link.cpp
        src/tbb/itt_notify.cpp
        src/tbb/cache_aligned_allocator.cpp
        src/tbb/pipeline.cpp
        src/tbb/queuing_mutex.cpp
        src/tbb/queuing_rw_mutex.cpp
        src/tbb/reader_writer_lock.cpp
        src/tbb/spin_rw_mutex.cpp
        src/tbb/x86_rtm_rw_mutex.cpp
        src/tbb/spin_mutex.cpp
        src/tbb/critical_section.cpp
        src/tbb/mutex.cpp
        src/tbb/recursive_mutex.cpp
        src/tbb/condition_variable.cpp
        src/tbb/tbb_thread.cpp
        src/tbb/concurrent_monitor.cpp
        src/tbb/semaphore.cpp
        src/tbb/private_server.cpp
        src/rml/client/rml_tbb.cpp
        src/tbb/tbb_misc.cpp
        src/tbb/tbb_misc_ex.cpp
        src/tbb/task.cpp
        src/tbb/task_group_context.cpp
        src/tbb/governor.cpp
        src/tbb/market.cpp
        src/tbb/arena.cpp
        src/tbb/scheduler.cpp
        src/tbb/observer_proxy.cpp
        src/tbb/tbb_statistics.cpp
        src/tbb/tbb_main.cpp
        )

add_subdirectory(examples)