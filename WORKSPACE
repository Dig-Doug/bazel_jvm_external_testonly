load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")

http_archive(
    name = "com_google_protobuf",
    sha256 = "e62e394190bcfe62555e2d7b781f382adbcfa8595a3252b6676f9d3087874e4c",
    strip_prefix = "protobuf-d8e678aae4c77e32fe5e8e92046eb66f74dfd269",
    urls = [
        "https://github.com/protocolbuffers/protobuf/archive/d8e678aae4c77e32fe5e8e92046eb66f74dfd269.tar.gz",
    ],
)

http_archive(
    name = "io_grpc_grpc_java",
    sha256 = "233cb87bdfde16602b446a655d204b56772f2395ebf0a5dfa8c4500893adc7f9",
    strip_prefix = "grpc-java-57bc1910e4b23220e6a4b1f0f9326e5347e2ec41",
    urls = ["https://github.com/grpc/grpc-java/archive/57bc1910e4b23220e6a4b1f0f9326e5347e2ec41.tar.gz"],
)


http_archive(
    name = "rules_jvm_external",
    sha256 = "3d0e809a5a14cfe7e1071103e9e53528f2fa93e72b175fb43a8bdea74156382d",
    strip_prefix = "rules_jvm_external-0a7cc6a0b6764232a0ddd31ad87b489e1d47b166",
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/0a7cc6a0b6764232a0ddd31ad87b489e1d47b166.tar.gz",
)

http_archive(
    name = "rules_java",
    sha256 = "1969a89e8da396eb7754fd0247b7df39b6df433c3dcca0095b4ba30a5409cc9d",
    strip_prefix = "rules_java-32ddd6c4f0ad38a54169d049ec05febc393b58fc",
    urls = [
        "https://github.com/bazelbuild/rules_java/archive/32ddd6c4f0ad38a54169d049ec05febc393b58fc.tar.gz",
    ],
)

####################################
# Workspace setup

load("@rules_jvm_external//:defs.bzl", "maven_install")
load("@io_grpc_grpc_java//:repositories.bzl", "IO_GRPC_GRPC_JAVA_ARTIFACTS", "IO_GRPC_GRPC_JAVA_OVERRIDE_TARGETS")

# To update the pinned list of deps, use:
#  bazel run @unpinned_maven//:pin
maven_install(
    artifacts = [
        "org.apache.beam:beam-sdks-java-core:2.22.0",
        "org.apache.beam:beam-runners-direct-java:2.22.0",
        "org.apache.beam:beam-runners-google-cloud-dataflow-java:2.21.0",
        "org.apache.beam:beam-sdks-java-extensions-protobuf:2.22.0",
    ] + IO_GRPC_GRPC_JAVA_ARTIFACTS,
    fetch_sources = True,
    generate_compat_repositories = True,
    maven_install_json = "//:maven_install.json",
    override_targets = dict(
		    IO_GRPC_GRPC_JAVA_OVERRIDE_TARGETS.items() +
        {
            "io.grpc:grpc-all": "@io_grpc_grpc_java//api",
        }.items(),
    ),
    repositories = [
        "https://jcenter.bintray.com/",
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
)

load("@maven//:defs.bzl", "pinned_maven_install")

pinned_maven_install()

load("@maven//:compat.bzl", "compat_repositories")

compat_repositories()

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

bind(
    name = "guava",
    actual = "@maven//:com_google_guava_guava",
)

bind(
    name = "gson",
    actual = "@maven//:com_google_code_gson_gson",
)

bind(
    name = "error_prone_annotations",
    actual = "@maven//:com_google_errorprone_error_prone_annotations",
)

