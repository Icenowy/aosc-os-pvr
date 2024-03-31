project('xf86-video-pvrdri', 'c',
        default_options: [
            'buildtype=debugoptimized',
            'c_std=gnu99',
        ],
        version: '1.0',
        meson_version: '>= 0.56.0',
)

pvrdri_srcs = [
    'dri2.c',
    'driver.c',
    'drmmode_display.c',
    'dumb_bo.c',
    'pageflip.c',
    'present.c',
    'vblank.c',
]

libdrm_dep = dependency('libdrm', version: '>= 2.4.109')
xserver_dep = dependency('xorg-server', version: '>= 21.1')
gbm_dep = dependency('gbm', version: '>= 17.1')
epoxy_dep = dependency('gbm', version: '>= 1.5.4')
module_dir = xserver_dep.get_variable(pkgconfig : 'moduledir')

pvrdri_c_args = []
pvrdri_c_args += '-DWITH_LIBDRM=1'
pvrdri_c_args += '-DGLAMOR_HAS_EGL_QUERY_DMABUF=1'
pvrdri_c_args += '-DGLAMOR_HAS_EGL_QUERY_DRIVER=1'
pvrdri_c_args += '-DGLXEXT=1'
pvrdri_c_args += '-DGLAMOR=1'
pvrdri_c_args += '-DGLAMOR_HAS_GBM=1'
pvrdri_c_args += '-DGLAMOR_HAS_GBM_LINEAR=1'
pvrdri_c_args += '-DGBM_BO_WITH_MODIFIERS=1'

subdir('glamor')
subdir('glamor_egl')

shared_module(
    'pvrdri_drv',
    pvrdri_srcs,
    name_prefix: '',

    dependencies: [
        libdrm_dep,
        xserver_dep,
    ],
    c_args: pvrdri_c_args,
    link_with: [glamor, glamoregl],

    install: true,
    install_dir: join_paths(module_dir, 'drivers'),
)
