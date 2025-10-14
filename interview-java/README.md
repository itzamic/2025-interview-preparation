# Java 21 Exercises (Maven)

This module hosts Java exercises and tests using Java 21 with Maven and JUnit 5.

## Prerequisites
- JDK 21 (verify with: `java -version`)
- Maven 3.9+ (verify with: `mvn -version`)
- An IDE with Java support (VS Code + Java extensions or IntelliJ)

## Quick Start
- Run tests:
  - From this `interview-java/` directory: `mvn test`
- Run the example app:
  - `mvn -q -DskipTests exec:java`
- Run a single test:
  - `mvn -Dtest=AppTest test`
  - Or a pattern: `mvn -Dtest='*App*' test`

## Project Layout
- `src/main/java/com/interviewprep/...` — exercise implementations
- `src/test/java/com/interviewprep/...` — unit tests (JUnit 5)
- Entry point example:
  - `src/main/java/com/interviewprep/App.java`
  - `src/test/java/com/interviewprep/AppTest.java`

## Adding a New Exercise
1. Create your class under `src/main/java/com/interviewprep/exercises/<topic>/...`
2. Create the corresponding test under `src/test/java/com/interviewprep/exercises/<topic>/...`
3. Use JUnit 5 (`org.junit.jupiter.api.*`) and assertions from `org.junit.jupiter.api.Assertions`

Example:
- Main: `src/main/java/com/interviewprep/exercises/ds/Example.java`
- Test: `src/test/java/com/interviewprep/exercises/ds/ExampleTest.java`

Naming conventions:
- Tests should end with `*Test` (e.g., `ExampleTest`) so Maven Surefire picks them up by default.

## Build Details
- Java 21 is enforced via Maven Compiler Plugin (`release=21`).
- JUnit 5 via `org.junit.jupiter:junit-jupiter`.
- Surefire is configured for JUnit Platform.

You can view/edit Maven coordinates in `pom.xml`.

## Troubleshooting: Corporate Maven Mirror Errors
If you see errors like:
```
Could not transfer artifact ... from/to artifactory (https://artifactory.oci.oraclecorp.com/libs-release)
```
your local Maven is configured to use a corporate mirror (usually in `~/.m2/settings.xml`) that is not reachable.

Options to fix:
- Comment out or remove the corporate `<mirror>` temporarily; or
- Scope the mirror to exclude Central by setting:
  ```
  <mirrorOf>*,!central</mirrorOf>
  ```
- Or add a direct central mirror entry and ensure your corporate mirror doesn’t override central:
  ```
  <mirrors>
    <mirror>
      <id>corp</id>
      <url>https://artifactory.example.com/maven</url>
      <mirrorOf>external:*,!central</mirrorOf>
    </mirror>
    <mirror>
      <id>central-direct</id>
      <url>https://repo.maven.apache.org/maven2</url>
      <mirrorOf>central</mirrorOf>
    </mirror>
  </mirrors>
  ```
After updating `~/.m2/settings.xml`, re-run:
```
mvn -U -e -DskipTests validate
```
to refresh plugin and dependency metadata.

Note: Project-level `pom.xml` already declares Maven Central for dependencies and plugins, but a user `~/.m2/settings.xml` mirror overrides that; adjust your local settings accordingly.

## IDE Import
- Open this `interview-java/` folder as a Maven project in your IDE.
- If the IDE reports plugin resolution errors, apply the mirror fix above and reimport Maven.

## License
MIT (see repository root).
