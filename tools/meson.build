
if platform_windows
  gimp_debug_resume = executable('gimp-debug-resume',
    'gimp-debug-resume.c',
  )
endif


gimptool = executable('gimptool' + exec_ver,
  'gimptool.c',
  include_directories: rootInclude,
  dependencies: [
    gegl, gtk3,
  ],
  link_with: [
    libgimpbase,
  ],
  c_args: [
    '-DDATADIR="@0@"'.format(get_option('datadir')),
  ],
  install: true,
)

gimp_test_clipboard = executable('gimp-test-clipboard' + exec_ver,
  'gimp-test-clipboard.c',
  include_directories: rootInclude,
  dependencies: [
    gegl, gtk3,
  ],
  install: true,
)

if enable_default_bin and meson.version().version_compare('>=0.61.0')
  install_symlink(fs.name(gimptool.full_path()).replace(exec_ver, ''),
    pointing_to: fs.name(gimptool.full_path()),
    install_dir: get_option('bindir')
  )
  install_symlink(fs.name(gimp_test_clipboard.full_path()).replace(exec_ver, ''),
    pointing_to: fs.name(gimp_test_clipboard.full_path()),
    install_dir: get_option('bindir')
  )
endif

executable('kernelgen',
  'kernelgen.c',
  include_directories: rootInclude,
  install: false,
)

colorsvg2png = executable('colorsvg2png',
  'colorsvg2png.c',
  native: true,
  dependencies: [
    native_glib,
    native_rsvg
  ],
  # In case b_sanitize was set, we don't really care if the tool has issues (in
  # particular we experienced some memory leaks with b_sanitize=address, within
  # librsvg and we don't want this to break the build).
  override_options: [ 'b_sanitize=none' ],
  install: false,
)
