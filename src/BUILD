gen_rule(
    name='gen_version',
    cmd='sh build/version_info_linux.sh > $BUILD_DIR/version_string.ver',
    deps=[],
    outs=['$BUILD_DIR/version_string.ver']
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
    'rml/include',
  ],
  srcs = [
    'tbb/ia64-gas/atomic_support.s',
    'tbb/ia64-gas/lock_byte.s',
    'tbb/ia64-gas/log2.s',
    'tbb/ia64-gas/pause.s',
    'tbb/ia64-gas/ia64_misc.s',
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
    '../include',
    '.',
    'rml/include',
  ],
  srcs = [
    'tbb/concurrent_hash_map.cpp',
    'tbb/concurrent_queue.cpp',
    'tbb/concurrent_vector.cpp',
    'tbb/dynamic_link.cpp',
    'tbb/itt_notify.cpp',
    'tbb/cache_aligned_allocator.cpp',
    'tbb/pipeline.cpp',
    'tbb/queuing_mutex.cpp',
    'tbb/queuing_rw_mutex.cpp',
    'tbb/reader_writer_lock.cpp',
    'tbb/spin_rw_mutex.cpp',
    'tbb/x86_rtm_rw_mutex.cpp',
    'tbb/spin_mutex.cpp',
    'tbb/critical_section.cpp',
    'tbb/mutex.cpp',
    'tbb/recursive_mutex.cpp',
    'tbb/condition_variable.cpp',
    'tbb/tbb_thread.cpp',
    'tbb/concurrent_monitor.cpp',
    'tbb/semaphore.cpp',
    'tbb/private_server.cpp',
    'rml/client/rml_tbb.cpp',
    'tbb/tbb_misc.cpp',
    'tbb/tbb_misc_ex.cpp',
    'tbb/task.cpp',
    'tbb/task_group_context.cpp',
    'tbb/governor.cpp',
    'tbb/market.cpp',
    'tbb/arena.cpp',
    'tbb/scheduler.cpp',
    'tbb/observer_proxy.cpp',
    'tbb/tbb_statistics.cpp',
    'tbb/tbb_main.cpp',
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