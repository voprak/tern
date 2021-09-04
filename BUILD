load("@io_bazel_rules_go//go:def.bzl", "go_binary", "go_library", "go_test")
load("@bazel_gazelle//:def.bzl", "gazelle")

# gazelle:prefix github.com/jackc/tern
gazelle(name = "gazelle")

go_library(
    name = "tern_lib",
    srcs = [
        "copy_dir.go",
        "error_line_extract.go",
        "main.go",
        "ssh_tunnel.go",
    ],
    importpath = "github.com/jackc/tern",
    visibility = ["//visibility:private"],
    deps = [
        "//migrate",
        "@com_github_jackc_pgx_v4//:pgx",
        "@com_github_masterminds_sprig//:sprig",
        "@com_github_spf13_cobra//:cobra",
        "@com_github_vaughan0_go_ini//:go-ini",
        "@org_golang_x_crypto//ssh",
        "@org_golang_x_crypto//ssh/agent",
        "@org_golang_x_crypto//ssh/knownhosts",
    ],
)

go_binary(
    name = "tern",
    embed = [":tern_lib"],
    visibility = ["//visibility:public"],
)

go_test(
    name = "tern_test",
    srcs = [
        "error_line_extract_test.go",
        "tern_test.go",
    ],
    data = glob(["testdata/**"]),
    embed = [":tern_lib"],
    deps = [
        "@com_github_jackc_pgx_v4//:pgx",
        "@com_github_stretchr_testify//assert",
        "@com_github_stretchr_testify//require",
        "@com_github_vaughan0_go_ini//:go-ini",
    ],
)
