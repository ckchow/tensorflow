SOURCES = [
    "tif_stream.cxx"
]

prefix_dir = "tiff-4.0.6/libtiff"

genrule(
    name = "configure",
    srcs = glob(
        ["**/*"],
        exclude = [prefix_dir + "/tif_config.h"],
    ),
    outs = [prefix_dir + "/tif_config.h"],
    cmd = "pushd external/tif_archive/%s; workdir=$$(mktemp -d -t tmp.XXXXXXXXXX); cp -a * $$workdir; pushd $$workdir; ./configure --enable-shared=no --with-pic=no; popd; popd; cp $$workdir/tif_config_.h $(@D); rm -rf $$workdir;" % prefix_dir,
)

cc_library(
    name = "tif",
    srcs = [prefix_dir + "/" + source for source in SOURCES],
    hdrs = [prefix_dir + "/tiffio.hxx"] + [":configure"],
    includes = [prefix_dir],
    copts = ["-I" + prefix_dir + "/"],
    defines = [
        "HAVE_CONFIG_H",
    ],
    visibility = ["//visibility:public"],
)