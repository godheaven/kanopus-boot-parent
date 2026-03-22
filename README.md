<p style="text-align:left">
  <img src="https://www.kanopus.cl/assets/kanopus_black.png" width="220" alt="Kanopus logo"/>
</p>

![Maven](https://img.shields.io/maven-central/v/cl.kanopus/kanopus-boot-parent) ![License](https://img.shields.io/badge/license-Apache%20License,%20Version%202.0-blue) ![Java](https://img.shields.io/badge/java-17+-orange)

# kanopus-boot-parent

**Kanopus Boot Parent**  is the **central parent POM** for projects in the **Kanopus ecosystem** that build on top of *
*Spring Boot**.
It aggregates shared configuration, aligns dependency versions, and provides a consistent foundation for libraries and
applications.

## ✨ Features

This project provides a curated parent POM for Spring Boot modules with a set of common, configurable build
enhancements. The highlights below combine recent improvements and the long-standing capabilities provided by
the parent POM.

- 📦 Dependency management — Centralized versions for common libraries (Spring Boot, Lombok, JUnit, Mockito, etc.)

- 🔧 Build consistency — Shared configuration for compiler, test, and plugin behavior across modules to reduce
  accidental divergence.

- ♻️ Reduced duplication — Saves time by removing repetitive Maven configuration from individual projects.

- 🧩 Spring Boot alignment — Ensures compatibility with the selected Spring Boot release train and healthy
  dependency alignment.

- 🔐 Configurable licensing — Class and source license header checks are provided but optional. Consumers can
  enable or skip license verification per-build (see Configurable properties).

- 🛡️ Configurable ProGuard packaging — Optional ProGuard-based obfuscation/optimization step for release
  artifacts. This is configurable so you can skip it during iterative development or enable it for published
  releases.

- 📈 Integration test coverage (automated) — Integration tests are included in coverage collection so the overall
  coverage (unit + integration) can be enforced. The default minimum overall coverage is 80% (configurable).
  The JaCoCo check runs during the `verify` phase and requires the JaCoCo execution data file (for example
  `target/jacoco.exec`) which is produced when tests actually run.

- 🧹 Automatic code formatting — Spotless with Google Java Format (AOSP style, 4-space indent) to maintain
  consistent code style across repositories.

- 🔍 Security validation — Optional Snyk integration to locate known vulnerabilities in dependencies.

- 📊 Code quality validation — Optional Sonar scanner integration for comprehensive static analysis.

Notes:

- Many build behaviors are opt-in/opt-out via Maven properties so maintainers can adapt the parent POM to their
  CI/CD policies without forking.
- If JaCoCo reports a missing exec file ("Skipping JaCoCo execution due to missing execution data file"), ensure
  tests are executed (do not set `maven.test.skip=true`) and that the test phase which generates the JaCoCo data
  is being run before `verify`.

## 🚀 Installation

To use this parent in your Maven project, add the following to your `pom.xml`:

```xml

<parent>
	<groupId>cl.kanopus</groupId>
	<artifactId>kanopus-boot-parent</artifactId>
	<version>4.04.0</version>
</parent>

```

## ⚙️ Configurable properties

You can tune the parent POM's behavior with simple Maven properties. The table below summarizes the most
important properties, their defaults, and quick guidance.

| Property                  | Default | Description                                                                                           | Example                          |
|---------------------------|--------:|-------------------------------------------------------------------------------------------------------|----------------------------------|
| `maven.test.skip`         | `false` | If `true`, tests are skipped. Keep `false` to produce JaCoCo coverage data.                           | `-Dmaven.test.skip=false`        |
| `license.skip`            |  `true` | Skip license-header verification when `true`.                                                         | `-Dlicense.skip=true`            |
| `proguard.skip`           |  `true` | Skip ProGuard packaging/obfuscation when `true`.                                                      | `-Dproguard.skip=true`           |
| `jacoco.minimum.coverage` |  `0.80` | Overall minimum coverage threshold (unit + integration). Build fails if coverage is below this value. | `-Djacoco.minimum.coverage=0.85` |
| `spotless.check.skip`     | `false` | Skip Spotless checks when `true`. Useful for quick local builds.                                      | `-Dspotless.check.skip=true`     |
| `snyk.skip`               |  `true` | Skip Snyk vulnerability checks when `true`.                                                           | `-Dsnyk.skip=true`               |
| `sonar.skip`              |  `true` | Skip Sonar analysis during `verify` when `true`.                                                      | `-Dsonar.skip=true`              |

Important notes

- To allow JaCoCo to collect execution data you must run tests (so keep `maven.test.skip=false`). If you see
  "Skipping JaCoCo execution due to missing execution data file" it means the JaCoCo report data file (e.g.
  `target/jacoco.exec`) was not produced — usually because tests did not run or ran in a different lifecycle that
  didn't produce the expected output path.
- Coverage threshold applies to the combined metric (unit + integration tests) and is configurable via
  `jacoco.minimum.coverage`.

## 🚀 Usage Guide

Run full verification (default 80% coverage):

```bash
mvn -Dmaven.test.skip=false verify
```

Run verify with a 90% coverage threshold:

```bash
mvn -Djacoco.minimum.coverage=0.90 verify
```

Skip tests for a faster package step (no coverage data will be produced):

```bash
mvn -Dmaven.test.skip=true package
```

### Running Snyk and SonarQube Validations

Both Snyk and SonarQube require credentials to authenticate with their respective servers.

To run these validations, you need to configure the following environment variables:

- `SNYK_TOKEN`: Your API token generated from your Snyk account.
- `SONAR_TOKEN`: Your API token generated from your SonarQube server.

Then you can execute Maven and disable the skip flag:

**Linux/macOS:**

```bash
export SNYK_TOKEN="your-snyk-token"
export SONAR_TOKEN="your-sonar-token"
mvn verify -Dsnyk.skip=false -Dsonar.skip=false
```

**Windows (PowerShell):**

```powershell
$env:SNYK_TOKEN="your-snyk-token"
$env:SONAR_TOKEN="your-sonar-token"
mvn verify -Dsnyk.skip=false -Dsonar.skip=false
```

## 📚 When to use

Use Kanopus Boot Parent for modules that rely on Spring Boot.
For projects without Spring Boot, use kanopus-core-parent

## 👤 Author

⭐**Pablo Andrés Díaz Saavedra** — Founder of **Kanopus – Software Guided by the Stars**⭐

Kanopus is building a constellation of developers creating tools, libraries and platforms that simplify software
engineering.

[GitHub](https://github.com/godheaven) | [LinkedIn](https://www.linkedin.com/in/pablo-diaz-saavedra-4b7b0522/) | [Website](https://kanopus.cl)

## 📄 License

This software is licensed under the Apache License, Version 2.0. See the LICENSE file for details.
I hope you enjoy it.

[![Apache License, Version 2.0](https://img.shields.io/badge/license-Apache%20License%202.0-blue.svg)](https://opensource.org/license/apache-2-0)

## 🛟 Support

For support or questions contact: 📧 [soporte@kanopus.cl](mailto:soporte@kanopus.cl)
