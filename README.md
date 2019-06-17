# gradle-scala-library-howto
Because I don't know sbt...

Travis CI build status: [![Build Status](https://travis-ci.org/daggerok/gradle-scala-library-howto.svg?branch=master)](https://travis-ci.org/daggerok/gradle-scala-library-howto)

```bash
./gradlew clean test npm_i npm_run_build
```

[[toc]]

## gradle init

initialize new `scala` project:

```bash
mkdir gradle-scala-library-howto
cd gradle-scala-library-howto/
gradle init --type scala-library --package com.github.daggerok --project-name gradle-scala-library-howto --dsl kotlin
```

## gradle tests output

add to `build.gradle.kts` file these lines for better developer experience on tests execution:

```kotlin
import org.gradle.api.tasks.testing.logging.TestLogEvent.*

tasks {
    withType<Test> {
        testLogging {
            showExceptions = true
            showStandardStreams = true
            events(PASSED, SKIPPED, FAILED)
        }
    }
}
```

## gradle npm integration

add to `build.gradle.kts` file these lines for better developer experience on tests execution:

```kotlin
plugins {
    // Add Gradle NodeJS support
    id("com.moowork.node") version "1.3.1"
}

node {
    download = true
}
```

prepare everything together with npm scrips and use gradle instead:

```bash
./gradlew npm_i         # npm i
./gradlew npm_run build # npm run build
```

## publish project to GitHub

create `.gitignore` file:

```git
.idea/
*.iml
*.ipr
*.iws
*.log*
.gradle/
build/
/out/
.DS_Store
node_modules/
.vuepress/dist/
```

## Travis CI

just see [.travis.yml](.travis.yml) file as a the reference...
