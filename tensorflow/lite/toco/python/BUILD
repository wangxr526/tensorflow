package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

load("//tensorflow:tensorflow.bzl", "tf_py_wrap_cc")
load("//tensorflow:tensorflow.bzl", "tf_py_test")
load("//tensorflow:tensorflow.bzl", "py_binary")

cc_library(
    name = "toco_python_api",
    srcs = ["toco_python_api.cc"],
    hdrs = ["toco_python_api.h"],
    deps = [
        "//tensorflow/core:lib",
        "//tensorflow/lite/toco:model_flags_proto_cc",
        "//tensorflow/lite/toco:toco_flags_proto_cc",
        "//tensorflow/lite/toco:toco_graphviz_dump_options",
        "//tensorflow/lite/toco:toco_port",
        "//tensorflow/lite/toco:toco_tooling",
        "//third_party/python_runtime:headers",
    ],
)

tf_py_wrap_cc(
    name = "tensorflow_wrap_toco",
    srcs = ["toco.i"],
    deps = [
        ":toco_python_api",
        "//tensorflow/lite/toco:model_flags_proto_cc",
        "//tensorflow/lite/toco:toco_flags_proto_cc",
        "//third_party/python_runtime:headers",
        "@com_google_absl//absl/strings",
    ],
)

py_binary(
    name = "toco_from_protos",
    srcs = ["toco_from_protos.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":tensorflow_wrap_toco",
        "//tensorflow/python:platform",
    ],
)

tf_py_test(
    name = "toco_from_protos_test",
    srcs = ["toco_from_protos_test.py"],
    additional_deps = [
        "//tensorflow:tensorflow_py",
        "//tensorflow/lite/toco:model_flags_proto_py",
        "//tensorflow/lite/toco:toco_flags_proto_py",
    ],
    data = [
        ":toco_from_protos",
    ],
    tags = [
        "no_oss",
        "no_pip",
    ],
)
