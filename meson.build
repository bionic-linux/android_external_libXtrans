# SPDX-License-Identifier: MIT
# Copyright © 2021 Intel Corporation

project(
  'xtrans',
  ['c'],
  version : '1.4.0',
  meson_version : '>= 0.55.0',
  license : 'MIT AND MIT-open-group',
)

add_project_arguments(
  '-D_DEFAULT_SOURCE',
  '-D_BSD_SOURCE',
  language : 'c',
)

dep_xfuncproto = dependency('xproto')

cc = meson.get_compiler('c')

libcflags = []
foreach f : ['strcasecmp']
  if cc.has_function(f)
    libcflags += '-DHAVE_@0@'.format(f.to_upper())
  endif
endforeach

# Do we care about any platform that wouldn't have this?
extra_cflags = '-DHAS_STICKY_DIR_BIT'
if cc.has_function('fchown')
  extra_cflags = '-DHAS_FCHOWN'
endif

libxtrans = library(
  'Xtrans',
  [
    'Xtrans.c',
    'Xtranslcl.c',
    'Xtranssock.c',
    'Xtransutil.c',
    'transport.c',
  ],
  c_args : [libcflags, extra_cflags],
  dependencies : [dep_xfuncproto],
)

# TODO: subdir('doc')

import('pkgconfig').generate(
  libxtrans,
  name : 'XTrans',
  description : 'Abstract network code for X',
  extra_cflags : extra_cflags,
)
