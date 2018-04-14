gen_rule(
    name='gen_version',
    cmd='sh build/version_info_linux.sh >version_string.ver',
    deps=[],
    outs=['version_string.ver']
)

gen_rule(
    name='gen_tbbvars',
    cmd='sh build/generate_tbbvars.sh',
    deps=[],
    outs=[],
)

cc_library(
  name = '_tbb_ia64',
  incs = [
    'include',
    'src',
    'src/rml/include',
  ],
  srcs = [
    'src/tbb/ia64-gas/atomic_support.s',
    'src/tbb/ia64-gas/lock_byte.s',
    'src/tbb/ia64-gas/log2.s',
    'src/tbb/ia64-gas/pause.s',
    'src/tbb/ia64-gas/ia64_misc.s',
  ],
  extra_cppflags = ['-x assembler-with-cpp'],
  defs = [
    'DO_ITT_NOTIFY',
    'USE_PTHREAD',
    '__TBB_BUILD=1',
  ],
)

cc_library(
  name = 'tbb',
  incs = [
    'include',
    'src',
    'src/rml/include',
  ],
  srcs = [
    'src/tbb/concurrent_hash_map.cpp',
    'src/tbb/concurrent_queue.cpp',
    'src/tbb/concurrent_vector.cpp',
    'src/tbb/dynamic_link.cpp',
    'src/tbb/itt_notify.cpp',
    'src/tbb/cache_aligned_allocator.cpp',
    'src/tbb/pipeline.cpp',
    'src/tbb/queuing_mutex.cpp',
    'src/tbb/queuing_rw_mutex.cpp',
    'src/tbb/reader_writer_lock.cpp',
    'src/tbb/spin_rw_mutex.cpp',
    'src/tbb/x86_rtm_rw_mutex.cpp',
    'src/tbb/spin_mutex.cpp',
    'src/tbb/critical_section.cpp',
    'src/tbb/mutex.cpp',
    'src/tbb/recursive_mutex.cpp',
    'src/tbb/condition_variable.cpp',
    'src/tbb/tbb_thread.cpp',
    'src/tbb/concurrent_monitor.cpp',
    'src/tbb/semaphore.cpp',
    'src/tbb/private_server.cpp',
    'src/rml/client/rml_tbb.cpp',
    'src/tbb/tbb_misc.cpp',
    'src/tbb/tbb_misc_ex.cpp',
    'src/tbb/task.cpp',
    'src/tbb/task_group_context.cpp',
    'src/tbb/governor.cpp',
    'src/tbb/market.cpp',
    'src/tbb/arena.cpp',
    'src/tbb/scheduler.cpp',
    'src/tbb/observer_proxy.cpp',
    'src/tbb/tbb_statistics.cpp',
    'src/tbb/tbb_main.cpp',
  ],
  defs = [
    'DO_ITT_NOTIFY',
    'USE_PTHREAD',
    '__TBB_BUILD=1',
  ],
  # extra_cppflags = [
  # '-DDO_ITT_NOTIFY',
  #   '-DUSE_PTHREAD',
  #   '-D__TBB_BUILD=1',
  # ],
  deps = [
    ':gen_version',
    # ':_tbb_ia64',
    # '#openssl',
  ]
)