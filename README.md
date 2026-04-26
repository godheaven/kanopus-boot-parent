<p style="text-align:left">
  <img src="https://www.kanopus.cl/assets/kanopus_black.png" width="220" alt="Kanopus logo"/>
</p>

![Maven](https://img.shields.io/maven-central/v/cl.kanopus/kanopus-boot-parent) ![License](https://img.shields.io/badge/license-Apache%20License,%20Version%202.0-blue) ![Java](https://img.shields.io/badge/java-17+-orange)

# kanopus-boot-parent

**Kanopus Boot Parent** is the **Spring Boot-specific parent POM** for projects in the **Kanopus ecosystem**.
It extends [`kanopus-core-parent`](https://github.com/godheaven/kanopus-core-parent) — which provides all the
shared build infrastructure — and adds the Spring Boot layer: web starter, API documentation, repackaging, and
Spring Boot-aligned dependency overrides.

## 🏗️ Parent Hierarchy

```
org.springframework.boot:spring-boot-starter-parent
    └── cl.kanopus:kanopus-core-parent      ← shared build infrastructure, plugins, coverage, formatting…
            └── cl.kanopus:kanopus-boot-parent  ← Spring Boot web layer (this project)
                    └── your-project
```

> All plugin configuration (JaCoCo, Surefire, Failsafe, ProGuard, Spotless, Snyk, Sonar, etc.) is inherited
> from `kanopus-core-parent`. This POM only adds what is **exclusive to Spring Boot web modules**.

## ✨ Features

This project provides a curated parent POM for Spring Boot modules with a set of common, configurable build
enhancements.

- 📦 **Dependency management** — Centralized versions for common libraries (Spring Boot, Lombok, JUnit, Mockito,
  etc.) inherited from `kanopus-core-parent`.

- 🌐 **Spring Boot web layer** — Includes `spring-boot-starter-web` and `springdoc-openapi-starter-webmvc-ui`
  out of the box so every child module has REST and OpenAPI documentation ready to use.

- 🔧 **Build consistency** — Shared configuration for compiler, test, and plugin behavior across modules to
  reduce accidental divergence, fully inherited from `kanopus-core-parent`.

- ♻️ **Reduced duplication** — Saves time by removing repetitive Maven configuration from individual projects.

- 🧩 **Spring Boot alignment** — Ensures compatibility with the selected Spring Boot release train and healthy
  dependency alignment.

- 📦 **Configurable Spring Boot repackaging** — The `spring-boot-maven-plugin` repackage goal is managed here
  and can be skipped for library modules that must **not** produce a fat JAR (see `spring.boot.repackage.skip`).

- 🔐 **Configurable licensing** — Class and source license header checks are provided but optional. Consumers
  can enable or skip license verification per-build (see Configurable properties).

- 🛡️ **Configurable ProGuard packaging** — Optional ProGuard-based obfuscation/optimization step for release
  artifacts. Skippable during iterative development.

- 📈 **Integration test coverage (automated)** — Integration tests are included in coverage collection so the
  overall coverage (unit + integration) can be enforced. The default minimum overall coverage is **80%**
  (configurable). The JaCoCo check runs during the `verify` phase.

- 🧹 **Automatic code formatting** — Spotless with Google Java Format (AOSP style, 4-space indent) to maintain
  consistent code style across repositories.

- 🔍 **Security validation** — Optional Snyk integration to locate known vulnerabilities in dependencies.

- 📊 **Code quality validation** — Optional Sonar scanner integration for comprehensive static analysis.

- 🔒 **Proactive CVE patching** — Critical dependency overrides are applied centrally so all child modules
  are protected without extra configuration (see Security Fixes).

> **Note:** Many build behaviors are opt-in/opt-out via Maven properties so maintainers can adapt the parent
> POM to their CI/CD policies without forking.

## 🚀 Installation

To use this parent in your Maven project, add the following to your `pom.xml`:

```xml
<parent>
    <groupId>cl.kanopus</groupId>
    <artifactId>kanopus-boot-parent</artifactId>
    <version>4.06.3</version>
</parent>
```

## ⚙️ Configurable properties

You can tune the parent POM's behavior with simple Maven properties. All properties defined in
`kanopus-core-parent` are also available here (they are inherited).

| Property                    | Default | Description                                                                                            | Example                           |
|-----------------------------|--------:|--------------------------------------------------------------------------------------------------------|-----------------------------------|
| `spring.boot.repackage.skip`| `false` | Skip `spring-boot-maven-plugin` repackage goal. Set to `true` for **library** modules.                | `-Dspring.boot.repackage.skip=true` |
| `maven.test.skip`           | `false` | If `true`, tests are skipped. Keep `false` to produce JaCoCo coverage data.                           | `-Dmaven.test.skip=false`         |
| `license.skip`              |  `true` | Skip license-header verification when `true`.                                                          | `-Dlicense.skip=true`             |
| `proguard.skip`             |  `true` | Skip ProGuard packaging/obfuscation when `true`.                                                       | `-Dproguard.skip=true`            |
| `jacoco.minimum.coverage`   |  `0.80` | Overall minimum coverage threshold (unit + integration). Build fails if coverage is below this value.  | `-Djacoco.minimum.coverage=0.85`  |
| `spotless.check.skip`       | `false` | Skip Spotless checks when `true`. Useful for quick local builds.                                       | `-Dspotless.check.skip=true`      |
| `snyk.skip`                 |  `true` | Skip Snyk vulnerability checks when `true`.                                                            | `-Dsnyk.skip=true`                |
| `sonar.skip`                |  `true` | Skip Sonar analysis during `verify` when `true`.                                                       | `-Dsonar.skip=true`               |

> **Important:** To allow JaCoCo to collect execution data you must run tests (keep `maven.test.skip=false`).
> If you see *"Skipping JaCoCo execution due to missing execution data file"* it means `target/jacoco.exec`
> was not produced — usually because tests did not run or the `verify` phase was not reached.

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

Build a library module without producing a fat JAR:

```bash
mvn package -Dspring.boot.repackage.skip=true
```

### Running Snyk and SonarQube Validations

Both Snyk and SonarQube require credentials to authenticate with their respective servers.

To run these validations, configure the following environment variables:

- `SNYK_TOKEN`: Your API token generated from your Snyk account.
- `SONAR_TOKEN`: Your API token generated from your SonarQube server.

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

## 🔒 Security Fixes

The following CVE overrides are enforced centrally in this parent POM (managed in `kanopus-core-parent` or
here) so all child modules are automatically protected:

| CVE / Advisory | Severity | Affected Module | Patched Version | Description |
|---|---|---|---|---|
| `GHSA-72hv-8253-57qq` | MEDIUM | `tools.jackson.core:jackson-core` | `3.1.1` | Number Length Constraint Bypass in Async Parser (DoS) |
| `GHSA-6v53-7c9g-w56r` | HIGH | `tools.jackson.core:jackson-core` | `3.1.1` | Nesting Depth bypass in `UTF8DataInputJsonParser` |
| `GHSA-2m67-wjpj-xhg9` | HIGH | `tools.jackson.core:jackson-core` | `3.1.1` | Document Length constraint bypass in blocking, async and DataInput parsers |
| `CVE-2026-22741` | — | `org.springframework:spring-webmvc` | `7.0.7` | HTTP Request Smuggling via `spring-webmvc` |
| `CVE-2026-22737` | MEDIUM | `org.springframework:spring-webmvc` | `7.0.7` | Path traversal in Script View Templates |
| `CVE-2026-22735` | LOW | `org.springframework:spring-webmvc` | `7.0.7` | Stream corruption in Server-Sent Events (SSE) |

> These overrides are applied via `<properties>` (`spring-framework.version`, `jackson-core.version`) and
> `<dependencyManagement>`, ensuring the patched versions win over transitive resolutions from
> `springdoc-openapi-starter-webmvc-ui` and other third-party libraries.

## 📚 When to use

| Parent POM | Use when… |
|---|---|
| `kanopus-boot-parent` | Your module is a **Spring Boot web application or REST API** |
| `kanopus-core-parent` | Your module is a **library or utility** that does **not** require Spring Boot |

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
