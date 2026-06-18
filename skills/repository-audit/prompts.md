# Prompt Variants

## Короткий запуск

```text
Use the Repository Audit Skill. Full read-only audit. Russian report. Save to audit_reports/YYYY-MM-DD-audit-report.md.
```

## Глубокий запуск

```text
Use the Repository Audit Skill. Perform a deep layer-by-layer read-only audit of the whole repository. Start from the root structure and documentation, then inspect stack, dependencies, configs, architecture, runtime flows, tests, code quality, security/privacy, performance and developer experience. Do not modify code. Do not run build/test/lint/analyze/install commands. Save the report in Russian to audit_reports/YYYY-MM-DD-audit-report.md.
```

## Максимально строгий режим

```text
Use the Repository Audit Skill in strict read-only mode. You may only inspect files and run read-only commands. Do not run any command that executes project code. Do not modify anything except creating audit_reports/YYYY-MM-DD-audit-report.md. Mark all unverified claims as "Требует проверки".
```

## Только architecture focus

```text
Use the Repository Audit Skill. Perform read-only audit with extra focus on architecture, module boundaries, dependency direction, runtime flow and root causes. Still include the full report structure. Save to audit_reports/YYYY-MM-DD-audit-report.md.
```

## Только security/privacy focus

```text
Use the Repository Audit Skill. Perform read-only audit with extra focus on secrets, credentials, unsafe file/network/shell access, permissions and sensitive logging. Mask any possible secrets. Save to audit_reports/YYYY-MM-DD-audit-report.md.
```
