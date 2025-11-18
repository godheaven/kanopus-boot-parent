![Logo](https://www.kanopus.cl/admin/javax.faces.resource/images/logo-gray.png.xhtml?ln=paradise-layout)


[![Maven Central](https://img.shields.io/maven-central/v/cl.kanopus/kanopus-boot-parent.svg?label=Maven%20Central)](https://central.sonatype.com/artifact/cl.kanopus/kanopus-boot-parent)

## 📌 Overview

**Kanopus Boot Parent**  is the **central parent POM** for projects in the **Kanopus ecosystem** that build on top of **Spring Boot**.
It aggregates shared configuration, aligns dependency versions, and provides a consistent foundation for libraries and applications.


## ✨ Features

📦 Dependency management
Centralized versions for commonly used libraries (Spring Boot, Lombok, JUnit, Mockito, etc.).

🔧 Build consistency
Standardized configuration for compiler, testing, and plugin management.

♻️ Reduced duplication
Eliminates repetitive setup across multiple modules and repositories.

🧩 Spring Boot alignment
Ensures compatibility with the selected Spring Boot release train.


## 🚀 Usage

To use this parent in your Maven project, add the following to your `pom.xml`:

```xml
<parent>
  <groupId>cl.kanopus</groupId>
  <artifactId>kanopus-boot-parent</artifactId>
  <version>3.5.7</version>
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
