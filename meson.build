project('Frfun7', 'cpp',
        version: '1',
        default_options: ['cpp_std=c++17', 'buildtype=release'],
        meson_version: '>=0.49')

cxx = meson.get_compiler('cpp')
gcc_syntax = cxx.get_argument_syntax() == 'gcc'

warnings = [
  '-Wall',
  '-Wextra',
  '-Wshadow',
]

cflags = gcc_syntax ? [
  warnings,
] : []

ldflags = [
]


host_cpu_family = host_machine.cpu_family()

if host_cpu_family.startswith('x86')
  if gcc_syntax
    cflags += ['-mfpmath=sse', '-msse2', '-DFRFUN7_X86=1']
  else
    cflags += ['-DFRFUN7_X86=1']
  endif
endif


host_system = host_machine.system()

if gcc_syntax and (host_system == 'windows' or host_system == 'cygwin')
  if host_cpu_family == 'x86'
    cflags += '-mstackrealign'
    ldflags += '-Wl,--kill-at'
  endif
endif



sources = [
  'src/frfun7.cpp',
]

deps = gcc_syntax ? [
  dependency('vapoursynth').partial_dependency(includes: true, compile_args: true),
] : []

shared_module('frfun7',
              sources,
              dependencies: deps,
              link_args: ldflags,
              cpp_args: cflags,
              install: true)
