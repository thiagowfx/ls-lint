load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

############################################################
# http archives ############################################
############################################################

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "6b65cb7917b4d1709f9410ffe00ecf3e160edf674b78c54a894471320862184f",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.39.0/rules_go-v0.39.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.39.0/rules_go-v0.39.0.zip",
    ],
)

http_archive(
    name = "bazel_gazelle",
    sha256 = "ecba0f04f96b4960a5b250c8e8eeec42281035970aa8852dda73098274d14a1d",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.29.0/bazel-gazelle-v0.29.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.29.0/bazel-gazelle-v0.29.0.tar.gz",
    ],
)

http_archive(
    name = "rules_pkg",
    sha256 = "8f9ee2dc10c1ae514ee599a8b42ed99fa262b757058f65ad3c384289ff70c4b8",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_pkg/releases/download/0.9.1/rules_pkg-0.9.1.tar.gz",
        "https://github.com/bazelbuild/rules_pkg/releases/download/0.9.1/rules_pkg-0.9.1.tar.gz",
    ],
)

http_archive(
    name = "aspect_rules_js",
    sha256 = "08061ba5e5e7f4b1074538323576dac819f9337a0c7d75aee43afc8ae7cb6e18",
    strip_prefix = "rules_js-1.26.1",
    url = "https://github.com/aspect-build/rules_js/releases/download/v1.26.1/rules_js-v1.26.1.tar.gz",
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

############################################################
# custom repositories ######################################
############################################################

load("//:repositories.bzl", "go_repositories")

# gazelle:repository_macro repositories.bzl%go_repositories
go_repositories()

############################################################
# go #######################################################
############################################################

go_rules_dependencies()

go_register_toolchains(version = "1.20.4")

############################################################
# gazelle ##################################################
############################################################

gazelle_dependencies()

############################################################
# rules_pkg ################################################
############################################################

load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")

rules_pkg_dependencies()

############################################################
# rules_js #################################################
############################################################

load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_js_dependencies()

load("@rules_nodejs//nodejs:repositories.bzl", "DEFAULT_NODE_VERSION", "nodejs_register_toolchains")

nodejs_register_toolchains(
    name = "nodejs",
    node_version = DEFAULT_NODE_VERSION,
)

load("@aspect_rules_js//npm:repositories.bzl", "npm_translate_lock", "pnpm_repository")

npm_translate_lock(
    name = "npm",
    pnpm_lock = "//deployments/npm:pnpm-lock.yaml",
)

load("@npm//:repositories.bzl", "npm_repositories")

npm_repositories()

pnpm_repository(name = "pnpm")

############################################################
# github cli ###############################################
############################################################

http_archive(
    name = "com_github_cli_cli_darwin_arm64",
    build_file_content = """exports_files(glob(["bin/*"]))""",
    sha256 = "38ca9a355376abd1475362cf8b3cacf2a757198fe5fe70349cb1767666abacc6",
    strip_prefix = "gh_2.29.0_macOS_arm64",
    urls = [
        "https://github.com/cli/cli/releases/download/v2.29.0/gh_2.29.0_macOS_arm64.zip",
    ],
)

http_archive(
    name = "com_github_cli_cli_linux_amd64",
    build_file_content = """exports_files(glob(["bin/*"]))""",
    sha256 = "9fe05f43a11a7bf8eacf731422452d1997e6708d4160ef0efcb13c103320390e",
    strip_prefix = "gh_2.29.0_linux_amd64",
    urls = [
        "https://github.com/cli/cli/releases/download/v2.29.0/gh_2.29.0_linux_amd64.tar.gz",
    ],
)
