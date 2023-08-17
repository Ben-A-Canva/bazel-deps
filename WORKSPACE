workspace(name = "com_github_johnynek_bazel_deps")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl",
     "git_repository", "new_git_repository")

http_archive(
    name = "bazel_skylib",
    sha256 = "7832382668c6dde9f57e18923763a24f9087cac66a50fbcc5afca848d03f2aa1",
    strip_prefix = "bazel-skylib-b113ed5d05ccddee3093bb157b9b02ab963c1c32",
    urls = ["https://github.com/bazelbuild/bazel-skylib/archive/b113ed5d05ccddee3093bb157b9b02ab963c1c32.tar.gz"],
)


http_archive(
    name = "io_bazel_rules_scala",
    sha256 = "6982e330f48517461f231ea596bd93416200286ab73fc070a11052496689f0ee",
    strip_prefix = "rules_scala-5.1.0",
    url = "https://github.com/bazelbuild/rules_scala/releases/download/v5.1.0/rules_scala-v5.1.0.tar.gz",
)

load("@io_bazel_rules_scala//:scala_config.bzl", "scala_config")

scala_config()

load("@io_bazel_rules_scala//scala:scala.bzl", "scala_repositories")

scala_repositories()
register_toolchains("//:scala_toolchain")

# TODO(Jonathon): This pre-fetching of zlib, and reworking of com_google_protobuf
# is a temporary hack (found in https://github.com/bazelbuild/rules_scala/issues/726)
# that is used to avoid compiling Protobuf from source. Need this until our C++ toolchain is fixed because
# right now we can't compile Protobuf on our Mac Pros.



PROTOBUF_JAVA_VERSION = "3.6.1"

# http_archive(
#     name = "com_google_protobuf",
#     url = "https://repo1.maven.org/maven2/com/google/protobuf/protobuf-java/%s/protobuf-java-%s.jar" % (PROTOBUF_JAVA_VERSION, PROTOBUF_JAVA_VERSION),
#     build_file_content = """
# package(default_visibility = ["//visibility:public"])

# filegroup(
#     name = "meta",
#     srcs = glob([
#         "META-INF/**/*",
#     ])
# )

# filegroup(
#     name = "classes",
#     srcs = glob([
#         "com/**/*",
#         "google/**/*",
#     ])
# )

# genrule(
#     name = "protobuf_java",
#     srcs = [":meta", ":classes"],
#     outs = ["myjar.jar"],
#     toolchains = ["@bazel_tools//tools/jdk:current_java_runtime"],
#     cmd = "mkdir -p META-INF && mkdir -p com/google/protobuf && cp -r $(locations :meta) META-INF && cp -r $(locations :classes) com/google/protobuf && $(JAVABASE)/bin/jar cfM $@ META-INF com",
# )
#     """,
# )

http_archive( 
     name = "com_google_protobuf", 
     sha256 = "9510dd2afc29e7245e9e884336f848c8a6600a14ae726adb6befdb4f786f0be2", 
     urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.6.1.3.zip"], 
     strip_prefix = "protobuf-3.6.1.3", 
 ) 

####################################################################################################
# Scala rules
####################################################################################################



load("//3rdparty:workspace.bzl", "maven_dependencies")

maven_dependencies()


load("//3rdparty:target_file.bzl", "build_external_workspace")
build_external_workspace(name = "third_party")
bind(name = 'io_bazel_rules_scala/dependency/scalatest/scalatest', actual = '//3rdparty/jvm/org/scalatest')
