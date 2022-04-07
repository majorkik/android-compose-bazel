# Workspace name
workspace(name = "android-compose-bazel")

# Base
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Versions
KOTLIN_VERSION = "1.5.21"

COMPOSE_VERSION = "1.0.2"

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
        sha256 = "f3313afdd6abf1b8c75c6292f4e41f2dbafefc8f6c72762c7ba9b3daeef5da59",
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

# Dependencies
load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = [
        "org.jetbrains.kotlin:kotlin-stdlib:%s" % KOTLIN_VERSION,
        "androidx.core:core-ktx:1.7.0",
        "androidx.compose.ui:ui:%s" % COMPOSE_VERSION,
        "androidx.compose.material:material:%s" % COMPOSE_VERSION,
        "androidx.compose.ui:ui-tooling:%s" % COMPOSE_VERSION,
        "androidx.compose.ui:ui-tooling-preview:%s" % COMPOSE_VERSION,
        "androidx.compose.compiler:compiler:%s" % COMPOSE_VERSION,
        "androidx.compose.runtime:runtime:%s" % COMPOSE_VERSION,
        "androidx.lifecycle:lifecycle-runtime-ktx:2.3.1",
        "androidx.activity:activity-compose:1.3.1",
    ],
    override_targets = {
        "org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm": "@//:kotlinx_coroutines_core_jvm",
    },
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
)

# Secondary maven repository used mainly for workarounds
maven_install(
    name = "maven_secondary",
    artifacts = [
        # Workaround to add missing 'sun.misc' dependencies to 'kotlinx-coroutines-core-jvm' artifact
        # Check root BUILD file and 'override_targets' arg of a primary 'maven_install'
        "org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm:1.5.1",
    ],
    fetch_sources = True,
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
)
