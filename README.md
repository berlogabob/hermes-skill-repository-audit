# Hermes Repository Audit Skill

Read-only skill for auditing software repositories layer by layer and creating a Russian Markdown audit report.

## Features

- read-only repository audit;
- Russian audit report;
- top-down repository orientation;
- architecture review;
- dependency and configuration review;
- runtime flow review;
- test review;
- code quality review;
- security and privacy review;
- performance risk review;
- root cause analysis;
- local Markdown report saved to `audit_reports/YYYY-MM-DD-audit-report.md`.

## Install

Copy this folder:

```text
skills/repository-audit/
```

to your Hermes skills directory.

## Usage

Basic prompt:

```text
Use the Repository Audit Skill. Perform a full read-only audit of this repository. Do not modify source code. Do not run build, test, analyze, lint, install, or formatter commands. Create the audit report in Russian and save it to audit_reports/YYYY-MM-DD-audit-report.md.
```

## Scope

This skill is universal. It can be used with Flutter, Python, JavaScript/TypeScript, Hugo, Go, Rust, Java, C/C++, mixed repositories and other codebases.

## Safety Rules

The skill is intentionally read-only.

It must not:

- modify source code;
- format files;
- run tests;
- run builds;
- run package installs;
- run linters;
- run analyzers;
- delete, rename, or move project files.

The only allowed write operation is creating:

```text
audit_reports/YYYY-MM-DD-audit-report.md
```

## Repository Status

Current version: `0.1.0`



## License

MIT
