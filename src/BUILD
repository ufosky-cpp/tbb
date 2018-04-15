gen_rule(
    name='gen_version',
    cmd='sh build/version_info_linux.sh > $BUILD_DIR/version_string.ver',
    deps=[],
    outs=['$BUILD_DIR/version_string.ver']
)

cc_library(
  name = 'tbb',
  incs = [
    '../include',
    '.',
    'rml/include',
  ],
  export_incs = [
    '../include',
  ],
  srcs = [
    'tbb/arena.cpp',
    'tbb/cache_aligned_allocator.cpp',
    'tbb/concurrent_hash_map.cpp',
    'tbb/concurrent_monitor.cpp',
    'tbb/concurrent_queue.cpp',
    'tbb/concurrent_vector.cpp',
    'tbb/condition_variable.cpp',
    'tbb/critical_section.cpp',
    'tbb/dynamic_link.cpp',
    'tbb/governor.cpp',
    'tbb/itt_notify.cpp',
    'tbb/market.cpp',
    'tbb/mutex.cpp',
    'tbb/observer_proxy.cpp',
    'tbb/pipeline.cpp',
    'tbb/private_server.cpp',
    'tbb/queuing_mutex.cpp',
    'tbb/queuing_rw_mutex.cpp',
    'tbb/reader_writer_lock.cpp',
    'tbb/recursive_mutex.cpp',
    'tbb/scheduler.cpp',
    'tbb/semaphore.cpp',
    'tbb/spin_mutex.cpp',
    'tbb/spin_rw_mutex.cpp',
    'tbb/task.cpp',
    'tbb/task_group_context.cpp',
    'tbb/tbb_main.cpp',
    'tbb/tbb_misc.cpp',
    'tbb/tbb_misc_ex.cpp',
    'tbb/tbb_statistics.cpp',
    'tbb/tbb_thread.cpp',
    'tbb/x86_rtm_rw_mutex.cpp',
    'rml/client/rml_tbb.cpp',
    'old/concurrent_queue_v2.cpp',
    'old/concurrent_vector_v2.cpp',
    'old/spin_rw_mutex_v2.cpp',
    'old/task_v2.cpp',
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
    '#dl',
    '#pthread',
    '#rt',
  ]
)

cc_library(
  name = 'tbbmalloc',
  incs = [
    '../include',
    '.',
  ],
  export_incs = [
    '../include',
  ],
  srcs = [
    'tbbmalloc/backend.cpp',
    'tbbmalloc/backref.cpp',
    'tbbmalloc/frontend.cpp',
    'tbbmalloc/large_objects.cpp',
    'tbbmalloc/tbbmalloc.cpp',
    'tbb/itt_notify.cpp',
  ],
  defs = [
    'DO_ITT_NOTIFY',
    'USE_PTHREAD',
    '__TBBMALLOC_BUILD=1',
  ],
  deps = [
    ':gen_version',
    '#dl',
    '#pthread',
    '#rt',
  ]
)

cc_library(
  name = 'tbbmalloc_proxy',
  incs = [
    '../include',
    '.',
  ],
  export_incs = [
    '../include',
  ],
  srcs = [
    'tbbmalloc/proxy.cpp',
    'tbbmalloc/tbb_function_replacement.cpp',
  ],
  defs = [
    'DO_ITT_NOTIFY',
    'USE_PTHREAD',
    '__TBBMALLOC_BUILD=1',
  ],
  deps = [
    ':tbbmalloc',
  ]
)
