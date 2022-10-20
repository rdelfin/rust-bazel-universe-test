WORKSPACE_NAME = "rust-bazel-universe-test"

workspace(name = WORKSPACE_NAME)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_rust",
    sha256 = "0cc7e6b39e492710b819e00d48f2210ae626b717a3ab96e048c43ab57e61d204",
    urls = [
        "https://github.com/bazelbuild/rules_rust/releases/download/0.10.0/rules_rust-v0.10.0.tar.gz",
    ],
)

# Rust

load("@rules_rust//rust:repositories.bzl", "rust_repositories")

rust_repositories(
    edition = "2021",
    version = "1.64.0",
)

load("@rules_rust//tools/rust_analyzer:deps.bzl", "rust_analyzer_deps")

rust_analyzer_deps()

# Loads all 3rdparty crates
load("@rules_rust//crate_universe:repositories.bzl", "crate_universe_dependencies")
crate_universe_dependencies()

load("@rules_rust//crate_universe:defs.bzl", "crate", "crates_repository")
crates_repository(
    name = "crate_index",
    lockfile = "//:Cargo.Bazel.lock",
    cargo_lockfile = "//:Cargo.lock",
    packages = {
        "cxxbridge-cmd": crate.spec(version = "1.0.79"),
    },
)

load("@crate_index//:defs.bzl", "crate_repositories")
crate_repositories()
