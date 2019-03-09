# multidim_image_augmentation provides Tensorflow operations for 2D & 3D
# image augmentation.

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

cc_library(
    name = "types",
    hdrs = ["platform/types.h"],
)

cc_library(
    name = "bspline",
    hdrs = ["kernels/bspline.h"],
    deps = [
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_library(
    name = "cubic_interpolation",
    hdrs = ["kernels/cubic_interpolation.h"],
    deps = [
        ":bspline",
    ],
)

cc_library(
    name = "apply_deformation",
    hdrs = ["kernels/apply_deformation.h"],
    deps = [
        ":types",
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_library(
    name = "ops_hdrs",
    hdrs = ["ops/apply_deformation_ops.h"],
)

cc_library(
    name = "augmentation_ops_interfaces",
    srcs = [
        "ops/apply_deformation_ops.cc",
        "ops/apply_tabulated_functions_op.cc",
        "ops/cubic_interpolation1d_op.cc",
        "ops/cubic_interpolation2d_op.cc",
        "ops/cubic_interpolation3d_op.cc",
        "ops/random_lut_controlpoints_op.cc",
    ],
    linkstatic = 1,
    visibility = ["//visibility:public"],
    deps = [
        ":ops_hdrs",
        ":types",
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
    alwayslink = 1,
)

cc_library(
    name = "augmentation_ops_kernels",
    srcs = [
        "kernels/apply_deformation_ops.cc",
        "kernels/apply_tabulated_functions_op.cc",
        "kernels/cubic_interpolation_ops.cc",
        "kernels/random_lut_controlpoints_op.cc",
    ],
    hdrs = ["ops/apply_deformation_ops.h"],
    visibility = ["//visibility:public"],
    deps = [
        ":apply_deformation",
        ":cubic_interpolation",
        ":ops_hdrs",
        ":types"
    ],
    alwayslink = 1,
)

cc_library(
    name = "augmentation_ops_interfaces_and_kernels",
    visibility = ["//visibility:public"],
    deps = [
        ":augmentation_ops_interfaces",
        ":augmentation_ops_kernels",
    ],
)

# WARNING: Run with -D_GLIBCXX.. to ensure it works with your local TF.
cc_library(
    name = "python/ops/_augmentation_ops.so",
    srcs = [
        "ops/apply_deformation_ops.cc",
        "ops/apply_tabulated_functions_op.cc",
        "ops/cubic_interpolation1d_op.cc",
        "ops/cubic_interpolation2d_op.cc",
        "ops/cubic_interpolation3d_op.cc",
        "ops/random_lut_controlpoints_op.cc",
    ],
    deps = [
        ":augmentation_ops_kernels",
        ":types",
    ],
    copts = ["-pthread", "-std=c++11", "-D_GLIBCXX_USE_CXX11_ABI=0"]
)

## Python API
# Had to remove the op wrapper since it is only available if you build TF.
py_library(
    name = "augmentation_ops",
    srcs = [
        "__init__.py"
    ],
    data = [":python/ops/_augmentation_ops.so"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
)

py_test(
    name = "python/kernel_tests/apply_deformation_op_test",
    size = "medium",
    srcs = ["python/kernel_tests/apply_deformation_op_test.py"],
    deps = [
        ":augmentation_ops",
    ],
)

py_test(
    name = "python/kernel_tests/cubic_interpolation1d_op_test",
    size = "medium",
    srcs = ["python/kernel_tests/cubic_interpolation1d_op_test.py"],
    deps = [
        ":augmentation_ops",
    ],
)

py_test(
    name = "python/kernel_tests/cubic_interpolation2d_op_test",
    size = "medium",
    srcs = ["python/kernel_tests/cubic_interpolation2d_op_test.py"],
    deps = [
        ":augmentation_ops",
    ],
)

py_test(
    name = "python/kernel_tests/cubic_interpolation3d_op_test",
    size = "medium",
    srcs = ["python/kernel_tests/cubic_interpolation3d_op_test.py"],
    deps = [
        ":augmentation_ops",
    ],
)

py_test(
    name = "python/kernel_tests/random_lut_controlpoints_op_test",
    srcs = ["python/kernel_tests/random_lut_controlpoints_op_test.py"],
    deps = [
        ":augmentation_ops",
           ],
)

py_test(
    name = "python/kernel_tests/apply_tabulated_functions_op_test",
    srcs = ["python/kernel_tests/apply_tabulated_functions_op_test.py"],
    deps = [
        ":augmentation_ops",
    ],
)

py_library(
    name = "deformation_utils",
    srcs = [
        "deformation_utils.py",
    ],
    visibility = ["//visibility:public"],
    deps = [
        ":augmentation_ops",
    ],
)

py_test(
    name = "deformation_utils_test",
    size = "small",
    srcs = ["deformation_utils_test.py"],
    deps = [
        ":deformation_utils",
    ],
)
