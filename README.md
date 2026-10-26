# Modernizing a Legacy Java Swing Application to React and Spring Boot with IBM Bob

This lab walks you through using **IBM Bob** to modernize a legacy Java Swing desktop application into a modern, web-based stack — step by step, with minimal manual effort.

## What You Will Build

The starting point is a **Java Swing patient management system**: a desktop GUI backed by a local database. By the end of the lab, you will have transformed it into a fully decoupled web application with a **React + Material UI frontend** and a **Spring Boot REST API backend**.

## What the Lab Covers

The lab is divided into four main sections:

1. **Running the Legacy Swing Application** — Clone and run the original desktop app to understand what you are modernizing.

2. **Java Upgrade** — Use the IBM Bob Java Modernization workflow to upgrade the project from Java 8 to Java 17, automatically apply OpenRewrite migration recipes, fix build issues, and remediate known CVE vulnerabilities in its dependencies.

3. **Swing to React** — Prompt Bob to convert the Swing UI into a React web application using Vite and Material UI, with a Spring Boot backend. Bob scaffolds the full project structure, wires up the REST API, and verifies database connectivity.

4. **Java Unit Tests** — Run the Java Unit Testing workflow on the new Spring Boot backend to install JaCoCo, generate a test strategy, and produce unit tests for all classes with code coverage reporting.

5. **Java Vulnerability Remediation** — Run a final vulnerability scan on the modernized backend and let Bob fix any remaining CVEs.

## Prerequisites

- **IBM Bob** with the **Java Premium Package** add-on enabled
- **Java 17** installed on your system

## Getting Started

Open the [`lab-guide.md`](./lab-guide.md) file and follow the steps in order.
