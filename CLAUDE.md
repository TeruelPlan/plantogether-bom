# CLAUDE.md

This file provides guidance to Claude when working with code in this repository.

## Overview

`plantogether-bom` is a Maven Bill of Materials (BOM) that centralizes the versions of all internal PlanTogether
libraries (`plantogether-common`, `plantogether-proto`). It has no code — only a `<dependencyManagement>` block.

All microservices import this BOM so that internal library versions are managed in one place, independently of the
build configuration in `plantogether-parent`.

## Commands

```bash
# Install to local Maven repo
mvn clean install

# Deploy to GitHub Packages
mvn deploy
```

## How to use in a microservice

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.plantogether</groupId>
            <artifactId>plantogether-bom</artifactId>
            <version>1.0.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

## Versioning

Update `plantogether-common.version` and/or `plantogether-proto.version` properties here whenever a new version of
those libraries is released. Then release a new version of this BOM.

## Architecture

```
plantogether-parent   ← build config only (Spring Boot, Java, plugins, third-party versions)
plantogether-bom      ← internal library versions only (common, proto)
microservices         ← inherit parent + import bom
```
