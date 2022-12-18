workspace(name = "gazelle_rust")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# versions of dependencies
load(":deps_versions.bzl", "GAZELLE_SHA256", "GAZELLE_VERSION", "RULES_GO_SHA256", "RULES_GO_VERSION")

# Go/Gazelle

http_archive(
    name = "io_bazel_rules_go",
    sha256 = RULES_GO_SHA256,
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v{0}/rules_go-v{0}.zip".format(RULES_GO_VERSION),
        "https://github.com/bazelbuild/rules_go/releases/download/v{0}/rules_go-v{0}.zip".format(RULES_GO_VERSION),
    ],
)

http_archive(
    name = "bazel_gazelle",
    patches = [
        # this patch is needed for unused crate detection
        "//patches:bazel-gazelle.patch",
    ],
    sha256 = GAZELLE_SHA256,
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v{0}/bazel-gazelle-v{0}.tar.gz".format(GAZELLE_VERSION),
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v{0}/bazel-gazelle-v{0}.tar.gz".format(GAZELLE_VERSION),
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

go_rules_dependencies()

go_register_toolchains(
    nogo = "@//:nogo",
    version = "1.18.3",
)

gazelle_dependencies()

# Rust

http_archive(
    name = "rules_rust",
    patches = ["//patches:rules_rust.patch"],
    sha256 = "6bfe75125e74155955d8a9854a8811365e6c0f3d33ed700bc17f39e32522c822",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_rust/releases/download/0.9.0/rules_rust-v0.9.0.tar.gz",
        "https://github.com/bazelbuild/rules_rust/releases/download/0.9.0/rules_rust-v0.9.0.tar.gz",
    ],
)

load("@rules_rust//rust:repositories.bzl", "rules_rust_dependencies", "rust_register_toolchains")

rules_rust_dependencies()

rust_register_toolchains(
    edition = "2021",
    version = "1.63.0",
)

# gazelle_rust dependencies

load("//:deps1.bzl", "gazelle_rust_dependencies1")

gazelle_rust_dependencies1()

load("//:deps2.bzl", "gazelle_rust_dependencies2")

gazelle_rust_dependencies2()

# gazelle:repository_macro go_deps.bzl%go_dependencies
