project('WPEBackend', 'cpp', 'c',
	default_options: ['c_std=c99', 'cpp_std=c++11'],
	version: '0.1',
)

src = [
	'src/input.c',
	'src/loader.c',
	'src/pasteboard.c',
	'src/pasteboard-generic.cpp',
	'src/pasteboard-noop.cpp',
	'src/renderer-backend-egl.c',
	'src/renderer-host.c',
	'src/view-backend.c',
]
hdr = [
	'include/wpe/input.h',
	'include/wpe/loader.h',
	'include/wpe/pasteboard.h',
	'include/wpe/renderer-backend-egl.h',
	'include/wpe/renderer-host.h',
	'include/wpe/view-backend.h',
]


ccc = meson.get_compiler('c')
dep = []

if not ccc.has_header('EGL/eglplatform.h')
	dep += dependency('egl')
endif

if not ccc.has_function('dlopen')
	dep += ccc.find_library('dl')
endif

lib = shared_library('WPEBackend', src,
	include_directories: include_directories('include'),
	version: meson.project_version(),
	dependencies: dep,
	install: true)

install_headers(hdr, subdir: 'wpe')

import('pkgconfig').generate(
	name: 'wpe',
	description: 'The WPE library',
	libraries: lib,
	version: meson.project_version(),
)
