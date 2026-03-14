![Logo](https://www.kanopus.cl/assets/kanopus-grey.png)

[![Maven Central](https://img.shields.io/maven-central/v/cl.kanopus/kanopus-boot-parent.svg?label=Maven%20Central)](https://central.sonatype.com/artifact/cl.kanopus/kanopus-boot-parent)

## 📌 Overview

**Kanopus Boot Parent**  is the **central parent POM** for projects in the **Kanopus ecosystem** that build on top of *
*Spring Boot**.
It aggregates shared configuration, aligns dependency versions, and provides a consistent foundation for libraries and
applications.

## ✨ Features

📦 Dependency management
Centralized versions for commonly used libraries (Spring Boot, Lombok, JUnit, Mockito, etc.).

🔧 Build consistency
Standardized configuration for compiler, testing, and plugin management.

♻️ Reduced duplication
Eliminates repetitive setup across multiple modules and repositories.

🧩 Spring Boot alignment
Ensures compatibility with the selected Spring Boot release train.

🔐 Configurable license enforcement
Optional enforcement of license headers for source files. This behavior can be toggled so consumers can enable or skip
license checks during the build (see configurable properties).

🛡️ Configurable ProGuard packaging (obfuscation/optimization)
Optional ProGuard-based packaging to obfuscate and optimize artifacts during the build. This step is configurable and
can be skipped for faster iterative builds or enabled for release packaging.

📈 Automatic coverage for integration tests
Integration tests are included in the coverage verification pipeline so modules can enforce a minimum coverage level for
integration test code as well as unit tests. The minimum overall coverage threshold is configurable (default: `0.80`).
The JaCoCo check is intended to run during the `verify` phase and requires the JaCoCo execution data file (for example
`target/jacoco.exec`) produced when tests run.

🧹 Automatic code formatting
Integration with Spotless and Google Java Format (AOSP style, 4 spaces indent) to maintain consistent styling.

🔍 Security validation
Integrated Snyk plugin to locate vulnerabilities and security issues automatically.

📊 Code quality validation
Integrated Sonar scanner plugin for comprehensive code analysis.

## ⚙️ Configurable properties

You can adjust the build behavior using the following Maven properties (default values shown):

- `maven.test.skip` (default: `false`)
    - If set to `true`, Maven will skip executing tests. Keep it `false` to run tests and produce coverage data for
      JaCoCo.

- `license.skip` (default: `true`)
    - Controls whether license checks are skipped during the build.

- `proguard.skip` (default: `true`)
    - Controls whether ProGuard (obfuscation/optimization) is skipped.

- `jacoco.minimum.coverage` (default: `0.80`)
    - Minimum overall coverage threshold (e.g. `0.80` = 80%). The JaCoCo check will fail the build if total coverage is
      below this value.

- `spotless.check.skip` (default: `false`)
    - Controls whether the Spotless plugin validation should be skipped during the build.

- `snyk.skip` (default: `true`)
    - Controls whether the Snyk vulnerability check should be skipped.

- `sonar.skip` (default: `true`)
    - Controls whether the Sonar validation plugin should be skipped during the verification phase.

### Examples

- Run the full verification including JaCoCo check (default threshold):

```
mvn -Dmaven.test.skip=false verify
```

- Run verify with a 90% coverage threshold:

```
mvn -Djacoco.minimum.coverage=0.90 verify
```

- Skip tests for a faster package step:

```
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

## 🚀 Usage

To use this parent in your Maven project, add the following to your `pom.xml`:

```xml

<parent>
	<groupId>cl.kanopus</groupId>
	<artifactId>kanopus-boot-parent</artifactId>
	<version>4.03.0</version>
</parent>

```

## 📚 When to use

Use Kanopus Boot Parent for modules that rely on Spring Boot.
For projects without Spring Boot, use kanopus-core-parent

## Authors

- [@pabloandres.diazsaavedra](https://www.linkedin.com/in/pablo-diaz-saavedra-4b7b0522/)

## License

This software is licensed under the Apache License, Version 2.0. See the LICENSE file for details.
I hope you enjoy it.

[![Apache License, Version 2.0](https://img.shields.io/badge/license-Apache%20License%202.0-blue.svg)](https://opensource.org/license/apache-2-0)

## Support

For support, email soporte@kanopus.cl
