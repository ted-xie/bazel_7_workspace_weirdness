### rules_java 7.12.2 setup stanza
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "rules_java",
    urls = [
        "https://github.com/bazelbuild/rules_java/releases/download/7.12.2/rules_java-7.12.2.tar.gz",
    ],
    sha256 = "a9690bc00c538246880d5c83c233e4deb83fe885f54c21bb445eb8116a180b83",
)
load("@rules_java//java:repositories.bzl", "rules_java_dependencies", "rules_java_toolchains")
rules_java_dependencies()
rules_java_toolchains()

# rules_java 8.5.1 setup stanza
http_archive(
    name = "rules_java",
    urls = [
        "https://github.com/bazelbuild/rules_java/releases/download/8.5.1/rules_java-8.5.1.tar.gz",
    ],
    sha256 = "1389206b2208c5f33a05dd96e51715b0855c480c082b7bb4889a8e07fcff536c",
)

load("@rules_java//java:rules_java_deps.bzl", "rules_java_dependencies")
rules_java_dependencies()

# note that the following line is what is minimally required from protobuf for the java rules
# consider using the protobuf_deps() public API from @com_google_protobuf//:protobuf_deps.bzl
load("@com_google_protobuf//bazel/private:proto_bazel_features.bzl", "proto_bazel_features")  # buildifier: disable=bzl-visibility
proto_bazel_features(name = "proto_bazel_features")

# register toolchains
load("@rules_java//java:repositories.bzl", "rules_java_toolchains")
rules_java_toolchains()
