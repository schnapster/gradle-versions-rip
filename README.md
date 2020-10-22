Minimal reproduction project for https://github.com/ben-manes/gradle-versions-plugin/issues/432


Steps to reproduce:

1. Run `./gradlew dependencyUpdates` and notice that the output is as expected, recommending and update of the Spring Boot plugin from `2.4.0-M3` to `2.4.0-M4`:
```
gw dependencyUpdates

> Task :dependencyUpdates

------------------------------------------------------------
: Project Dependency Updates (report to plain text file)
------------------------------------------------------------

The following dependencies are using the latest milestone version:
 - com.github.ben-manes:gradle-versions-plugin:0.33.0

The following dependencies have later milestone versions:
 - org.springframework.boot:spring-boot-gradle-plugin [2.4.0-M3 -> 2.4.0-M4]

Gradle release-candidate updates:
 - Gradle: [6.7: UP-TO-DATE]

Generated report file build/dependencyUpdates/report.txt

BUILD SUCCESSFUL in 1s
1 actionable task: 1 executed
```

2. Edit `build.gradle` with the new Spring Boot version `2.4.0-M4` and save it.
3. Run `./gradlew dependencyUpdates` again, and notice how now certain resolutions fail to resolve:
```
gw dependencyUpdates

> Task :dependencyUpdates
Failed to resolve ::bootArchives
Failed to resolve ::implementation
Failed to resolve ::runtimeElements
Failed to resolve ::runtimeOnly
Failed to resolve ::testImplementation
Failed to resolve ::testRuntimeOnly

------------------------------------------------------------
: Project Dependency Updates (report to plain text file)
------------------------------------------------------------

The following dependencies are using the latest milestone version:
 - com.github.ben-manes:gradle-versions-plugin:0.33.0
 - org.springframework.boot:spring-boot-gradle-plugin:2.4.0-M4

Gradle release-candidate updates:
 - Gradle: [6.7: UP-TO-DATE]

Generated report file build/dependencyUpdates/report.txt

Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
Use '--warning-mode all' to show the individual deprecation warnings.
See https://docs.gradle.org/6.7/userguide/command_line_interface.html#sec:command_line_warnings

BUILD SUCCESSFUL in 1s
1 actionable task: 1 executed
```
