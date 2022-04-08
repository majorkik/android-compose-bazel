# <p align="center">Jetpack Compose with Bazel</p>
<p align="center">:rocket: A project using Basel as an additional build system</p>

<p align="center">
  <a>
    <img src="https://img.shields.io/badge/Android-32DE84?style=for-the-badge&logo=android&logoColor=white" alt="Android">
  </a>
  
  <a>
    <img src="https://img.shields.io/badge/Bazel%205.1.0-161616.svg?style=for-the-badge&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAABHNCSVQICAgIfAhkiAAAAW9JREFUKFN1kU1LAmEQx2eyWq2rFojooSyQ3ujirQ0D/RZB9yhBOqcfQKhP0Msn6NDJgyR0aK9aHrKgzU0CO4iRuej2tPPUyGbuXp5n5j+/+c/sg/D7ZaqZiKeP59a42M7H8jrn6RylIQtjPSwhYkQIoX9NCJVhgkZp6BTYhWGKGRrWcFfbu5nyKXHnaHTvfJoanW4aJs5S9aXYAngVb4jhrtk1bqv3MnTTcOs0JQSCwQUMoQDZyE2TIBdE5yPN2oMeYGiwl914WMPESTJr/81DKqo1XgpBvz82PakMxqb8x3vHaNTq1ej6YlKaCJGTz8Fw+UkvvbXac3F7Z4YJ0i6uwR+eeVxR11SCijuFrAQZrujPm81WW7WTBsFgWkCQABEKhGdLyxurVwRR/QCkQDkIH5m9/j7dPYga3L2CZVnyqRSfcmxemmk2+gPKZDpIHeXOUGn81AnIQRGkkzvohAkcAf0b1dlROpdtcMiJa74BmPnVW/Dy3dUAAAAASUVORK5CYII=&logoColor=white" alt="Bazel">
  </a>
  
  <a>
    <img src="https://img.shields.io/badge/Kotlin%201.6.10-F6891F?style=for-the-badge&logo=Kotlin&logoColor=white" alt="Kotlin">
  </a>
  
  <a>
    <img src="https://img.shields.io/badge/Jetpack%20Compose%201.2.0%20alpha06-1AA2D4?style=for-the-badge" alt="Kotlin">
  </a>  
</p>

## Rules
- [Android rules for Bazel](https://github.com/bazelbuild/rules_android)
- [Bazel Kotlin Rules](https://github.com/bazelbuild/rules_kotlin)
- [Bazel JVM Extenrla Rules](https://github.com/bazelbuild/rules_jvm_external) - Bazel rules to resolve, fetch and export Maven artifacts

## Build project

Use `bazel` or `bazelisk` to build a project

> Install [Basel](https://bazel.build) or [Basilisk](https://github.com/bazelbuild/bazelisk)(recommended) if they are not already installed following this [installation guide](https://bazel.build/install)

```bash
# Build the app module library
bazelisk build app:app-lib

# Build android binary
bazelisk build app:bin
```
