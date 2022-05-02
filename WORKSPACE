# Workspace name
workspace(name = "android-compose-bazel")

# Base
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Versions
KOTLIN_VERSION = "1.6.10"

COMPOSE_VERSION = "1.2.0-alpha06"

# Android
RULES_ANDROID_TAG = "0.1.1"

RULES_ANDROID_SHA = "cd06d15dd8bb59926e4d65f9003bfc20f9da4b2519985c27e190cddc8b7a7806"

http_archive(
    name = "rules_android",
    sha256 = RULES_ANDROID_SHA,
    strip_prefix = "rules_android-%s" % RULES_ANDROID_TAG,
    urls = ["https://github.com/bazelbuild/rules_android/archive/v%s.zip" % RULES_ANDROID_TAG],
)

android_sdk_repository(
    name = "androidsdk",
    api_level = 31,
    build_tools_version = "30.0.2",
)

# Kotlin
RULES_KOTLIN_TAG = "1.5.0"

RULES_KOTLIN_SHA = "12d22a3d9cbcf00f2e2d8f0683ba87d3823cb8c7f6837568dd7e48846e023307"

http_archive(
    name = "io_bazel_rules_kotlin",
    sha256 = RULES_KOTLIN_SHA,
    urls = ["https://github.com/bazelbuild/rules_kotlin/releases/download/v%s/rules_kotlin_release.tgz" % RULES_KOTLIN_TAG],
)

load("@io_bazel_rules_kotlin//kotlin:repositories.bzl", "kotlin_repositories", "kotlinc_version")

kotlin_repositories(
    compiler_release = kotlinc_version(
        release = KOTLIN_VERSION,
        sha256 = "432267996d0d6b4b17ca8de0f878e44d4a099b7e9f1587a98edc4d27e76c215a",
    ),
)

register_toolchains("//:kotlin_toolchain")

# JVM External
RULES_JVM_EXTERNAL_TAG = "4.2"

RULES_JVM_EXTERNAL_SHA = "cd1a77b7b02e8e008439ca76fd34f5b07aecb8c752961f9640dea15e9e5ba1ca"

http_archive(
    name = "rules_jvm_external",
    sha256 = RULES_JVM_EXTERNAL_SHA,
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
)

load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")

rules_jvm_external_deps()

load("@rules_jvm_external//:setup.bzl", "rules_jvm_external_setup")

rules_jvm_external_setup()

# Dependencies
load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = [
        "androidx.compose.foundation:foundation:%s" % COMPOSE_VERSION,
        "androidx.compose.animation:animation:%s" % COMPOSE_VERSION,
        "org.jetbrains.kotlin:kotlin-stdlib:%s" % KOTLIN_VERSION,
        "androidx.core:core-ktx:1.7.0",
        "androidx.compose.ui:ui:%s" % COMPOSE_VERSION,
        "androidx.compose.material:material:%s" % COMPOSE_VERSION,
        "androidx.compose.ui:ui-tooling:%s" % COMPOSE_VERSION,
        "androidx.compose.ui:ui-tooling-preview:%s" % COMPOSE_VERSION,
        "androidx.compose.compiler:compiler:%s" % COMPOSE_VERSION,
        "androidx.compose.runtime:runtime:%s" % COMPOSE_VERSION,
        "androidx.lifecycle:lifecycle-runtime-ktx:2.4.1",
        "androidx.activity:activity-compose:1.4.0",
    ],
    jetify = True,
    override_targets = {
        "org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm": "@//:kotlinx_coroutines_core_jvm",
    },
    repositories = [
        "https://maven.google.com/",
        "https://repo1.maven.org/maven2",
    ],
    # Resolving user-specified and transitive dependency version conflicts
    # pinned: pin the versions of the artifacts that are explicitly specified in maven_install.
    # It is necessary because of the version of Jetpack compose >= 1.2.0-alpha02
    # Perhaps the stable version of Jetpack Compose will fix this error
    version_conflict_policy = "pinned",
)

# Secondary maven repository used mainly for workarounds
# The versions must also match in /BUILD.bazel
KOTLINX_COROUTINES_VERSION = "1.6.0"

maven_install(
    name = "maven_secondary",
    artifacts = [
        # Workaround to add missing 'sun.misc' dependencies to 'kotlinx-coroutines-core-jvm' artifact
        # Check root BUILD file and 'override_targets' arg of a primary 'maven_install'
        "org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm:1.6.0",
    ],
    fetch_sources = True,
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
)
