project('hidapi', 'c', version : '0.8.0-rc1')

inc = include_directories('hidapi')

hidapi_sources = [
  'hidapi/hidapi.h'
]
hidapi_link_args = []
if host_machine.system() == 'windows'
  hidapi_sources += 'libusb/hid.c'
  cc = meson.get_compiler('c')

  libusbdll = cc.find_library('libusb-1.0', dirs : [join_paths(meson.current_source_dir(),'libusbdll')])
  libusbdll_inc = include_directories('libusbdll')

  hidapi_deps = [
    libusbdll,
    dependency('threads')
  ]
  hidapi_deps += cc.find_library('setupapi', required : true)
  hidapi_link_args += '-Wall'
elif host_machine.system() == 'linux'
  hidapi_sources += 'libusb/hid.c'
  hidapi_deps = [
    dependency('libusb-1.0', required : true),
    dependency('threads')
  ]
endif

libhidapi = shared_library(
  'hidapi',
  hidapi_sources,
  dependencies : hidapi_deps,
  include_directories : inc,
  link_args : hidapi_link_args,
  install : true
)

hidapi_dep = declare_dependency(
  include_directories : inc,
  link_with : libhidapi
)
