glamoregl_src = [
    '../glamor/glamor_egl.c',
    'glamor_xf86_xv.c',
]

glamoregl = static_library(
    'glamoregl',
    glamoregl_src,

    dependencies: [
        xserver_dep,
        libdrm_dep,
        gbm_dep,
    ],
    c_args: pvrdri_c_args,
)
