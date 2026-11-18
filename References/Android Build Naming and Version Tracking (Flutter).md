---
type: reference
created: 2026-11-18
domain: flutter
tags:
  - reference
  - flutter
  - android
  - gradle
---
# Android build naming & version tracking (for later use in other Flutter apps)

This describes the setup used in `android/app/build.gradle.kts` (Patient App) so it
can be reproduced in other Flutter projects, e.g. the Driver App.

## What it does

1. Tracks `VERSION_NAME` / `VERSION_CODE` in a `version.properties` file as the source
   of truth, auto-increments `VERSION_CODE` by 1 every time Gradle evaluates the app
   module (i.e. every `flutter build`/`flutter run` on Android), and writes the result
   back into `pubspec.yaml`'s `version:` line so both stay in sync.
2. After every APK/AAB build, copies the output into `<repo root>/Release/` with a
   descriptive, collision-free name instead of Flutter's generic `app-release.apk`.

## 1. Version tracking: `android/version.properties`

Create the file next to `android/build.gradle.kts` (repo-level `android/` folder):

```properties
VERSION_NAME=0.0.1
VERSION_CODE=1
```

Keep this file tracked in git (don't add it to `.gitignore`) so the version persists
across machines/CI.

In `android/app/build.gradle.kts`, read it, bump the code, and write it back at the
top of the script (before the `android {}` block):

```kotlin
import java.io.FileInputStream
import java.io.FileOutputStream
import java.util.Properties

val versionPropertiesFile = rootProject.file("version.properties")
val versionProperties = Properties().apply {
    FileInputStream(versionPropertiesFile).use { load(it) }
}
val appVersionName = versionProperties.getProperty("VERSION_NAME")
val appVersionCode = versionProperties.getProperty("VERSION_CODE").toInt() + 1
versionProperties.setProperty("VERSION_CODE", appVersionCode.toString())
FileOutputStream(versionPropertiesFile).use { versionProperties.store(it, null) }

// Keep pubspec.yaml's version in sync so `flutter` tooling reports the same value.
val pubspecFile = rootProject.projectDir.parentFile.resolve("pubspec.yaml")
pubspecFile.writeText(
    pubspecFile.readText().replace(
        Regex("(?m)^version:\\s*\\S+$"),
        "version: $appVersionName+$appVersionCode",
    )
)
```

Then wire it into `defaultConfig` instead of `flutter.versionCode` / `flutter.versionName`:

```kotlin
defaultConfig {
    // ...
    versionCode = appVersionCode
    versionName = appVersionName
}
```

Notes:
- `Properties.store(out, null)` writes a `#<timestamp>` comment line automatically —
  that's expected, not a bug.
- The increment happens at Gradle configuration time, so it fires on every Gradle
  invocation that touches this module (builds, not just `assemble`/`bundle`). This is
  intentional: simpler than hooking every build task, and in practice Gradle is only
  configured here when actually building/running the Android app.

## 2. Named build output: copy APK/AAB into `Release/`

Add this after the `flutter { source = "../.." }` block in `android/app/build.gradle.kts`
(or split into its own applied script, e.g. `build-naming.gradle.kts`, via
`apply(from = "build-naming.gradle.kts")`):

```kotlin
import java.time.LocalDateTime
import java.time.format.DateTimeFormatter

// After each APK/AAB build, copies the output under the name
// <applicationId>_<versionName>_<versionCode>_<yyyyMMdd_HHmmss>.<apk|aab>
// (debug/profile builds get a -debug/-profile suffix, split ABIs keep theirs)
// into <repo root>/Release/.
// APKs are read from outputs/flutter-apk; bundles from outputs/bundle/<type>.
// Flutter's tool expects the original app-<type>.<ext> names, so those files
// are left untouched.
val releaseRootDir = rootProject.projectDir.parentFile.resolve("Release")

listOf("debug", "profile", "release").forEach { buildType ->
    val variant = buildType.replaceFirstChar { it.uppercase() }
    val baseName = listOf(
        android.defaultConfig.applicationId,
        android.defaultConfig.versionName,
        android.defaultConfig.versionCode,
    ).joinToString("_")

    // (gradle task to hook, extension, AGP output dir)
    listOf(
        listOf("assemble$variant", "apk", "outputs/apk/$buildType"),
        listOf("bundle$variant", "aab", "outputs/bundle/$buildType"),
    ).forEach { (hookTask, ext, srcPath) ->
        val srcDir = layout.buildDirectory.dir(srcPath)

        val copyNamed = tasks.register("copyNamed$variant${ext.replaceFirstChar { it.uppercase() }}") {
            doLast {
                val now = LocalDateTime.now()
                val stamp = now.format(DateTimeFormatter.ofPattern("yyyyMMdd_HHmmss"))
                val outDir = releaseRootDir.apply { mkdirs() }
                // Only pick up AGP's own app-*.<ext> outputs, not previously named copies.
                val files = srcDir.get().asFile.listFiles { file ->
                    file.extension == ext && file.name.startsWith("app-")
                } ?: return@doLast
                for (file in files) {
                    // "app-arm64-v8a-release.apk" -> "arm64-v8a"; "app-release.aab" -> "".
                    val abi = file.nameWithoutExtension.removePrefix("app-")
                        .removeSuffix(buildType).trimEnd('-')
                    val suffix = listOfNotNull(
                        abi.ifEmpty { null },
                        buildType.takeIf { it != "release" },
                    ).joinToString("") { "-$it" }
                    val target = outDir.resolve("${baseName}_$stamp$suffix.$ext")
                    file.copyTo(target, overwrite = true)
                    println("Named ${ext.uppercase()}: ${target.absolutePath}")
                }
            }
        }

        tasks.matching { it.name == hookTask }.configureEach {
            finalizedBy(copyNamed)
        }
    }
}
```

Add `/Release/` to the repo's `.gitignore` so these copies aren't committed.

## Porting checklist for another Flutter app

- [ ] Add `android/version.properties` with `VERSION_NAME`/`VERSION_CODE` seeded from
      the app's current `pubspec.yaml` version.
- [ ] Add the version-read/increment block to `android/app/build.gradle.kts`, before
      the `android {}` block.
- [ ] Point `defaultConfig.versionCode`/`versionName` at `appVersionCode`/`appVersionName`.
- [ ] Add the `Release/` copy block (or apply it from a separate script file).
- [ ] Add `/Release/` to `.gitignore`.
- [ ] Make sure `version.properties` itself is **not** gitignored — it must be tracked.
- [ ] Adjust `applicationId` references if the app's package name differs.

## Related
- [[create-android-project|create-android-project]] — Command reference for scaffolding a new Android/Flutter project.
- [[Technology Stack (Flutter)|Technology Stack (Flutter)]]
