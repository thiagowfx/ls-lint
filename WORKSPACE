load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

############################################################
# http archives ############################################
############################################################

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "278b7ff5a826f3dc10f04feaf0b70d48b68748ccd512d7f98bf442077f043fe3",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.41.0/rules_go-v0.41.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.41.0/rules_go-v0.41.0.zip",
    ],
)

http_archive(
    name = "bazel_gazelle",
    sha256 = "29218f8e0cebe583643cbf93cae6f971be8a2484cdcfa1e45057658df8d54002",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.32.0/bazel-gazelle-v0.32.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.32.0/bazel-gazelle-v0.32.0.tar.gz",
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
    sha256 = "e3e6c3d42491e2938f4239a3d04259a58adc83e21e352346ad4ef62f87e76125",
    strip_prefix = "rules_js-1.30.0",
    url = "https://github.com/aspect-build/rules_js/releases/download/v1.30.0/rules_js-v1.30.0.tar.gz",
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

go_register_toolchains(version = "1.20.5")

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
    npmrc = "//deployments/npm:.npmrc",
    pnpm_lock = "//deployments/npm:pnpm-lock.yaml",
)

load("@npm//:repositories.bzl", "npm_repositories")

npm_repositories()

pnpm_repository(name = "pnpm")

load("@aspect_bazel_lib//lib:repositories.bzl", "register_jq_toolchains")

register_jq_toolchains()

############################################################
# github cli ###############################################
############################################################

http_archive(
    name = "com_github_cli_cli_darwin_arm64",
    build_file_content = """exports_files(glob(["bin/*"]))""",
    sha256 = "88ef39440f594a996a6245a8ad0986f28e38acb9725118e3780f3ca8a10c447e",
    strip_prefix = "gh_2.31.0_macOS_arm64",
    urls = [
        "https://github.com/cli/cli/releases/download/v2.31.0/gh_2.31.0_macOS_arm64.zip",
    ],
)

http_archive(
    name = "com_github_cli_cli_linux_amd64",
    build_file_content = """exports_files(glob(["bin/*"]))""",
    sha256 = "eec349e43803759d3d7a138d214ae983a3bebebd8e6dd0ec0ff1eea7bdd823e7",
    strip_prefix = "gh_2.31.0_linux_amd64",
    urls = [
        "https://github.com/cli/cli/releases/download/v2.31.0/gh_2.31.0_linux_amd64.tar.gz",
    ],
)

############################################################
# coreutils (sha256) #######################################
############################################################

http_archive(
    name = "com_github_uutils_coreutils_darwin_arm64",
    build_file_content = """exports_files(["coreutils"])""",
    sha256 = "0d0f02f3ff59bc5490c915d3c4711234c69f5a84d7348f9cf4c67dc212a28923",
    strip_prefix = "coreutils-0.0.19-x86_64-apple-darwin",
    urls = [
        "https://github.com/uutils/coreutils/releases/download/0.0.19/coreutils-0.0.19-x86_64-apple-darwin.tar.gz",  # only amd64
    ],
)

http_archive(
    name = "com_github_uutils_coreutils_linux_amd64",
    build_file_content = """exports_files(["coreutils"])""",
    sha256 = "0eea02fe91ce43f24b21c5fb50ed45ae596c3c7978f777d82ea18d78d88ddbf4",
    strip_prefix = "coreutils-0.0.19-x86_64-unknown-linux-gnu",
    urls = [
        "https://github.com/uutils/coreutils/releases/download/0.0.19/coreutils-0.0.19-x86_64-unknown-linux-gnu.tar.gz",
    ],
)
