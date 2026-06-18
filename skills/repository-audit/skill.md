# Repository Audit Skill

Version: 0.1.0  
Language: Russian  
Mode: read-only audit

Use this skill when the user asks to audit, inspect, review, or deeply analyze a repository and create a structured audit report.

## Цель

Провести полный аудит репозитория сверху вниз:

1. понять проект на верхнем уровне;
2. разобрать структуру;
3. определить стек и архитектурные слои;
4. пройтись по зависимостям, конфигам, entry points, runtime flow;
5. найти проблемы;
6. докопаться до корневых причин;
7. сохранить полный отчёт локально в Markdown.

Аудит должен быть универсальным и подходить для любых стеков: Flutter, Python, JavaScript/TypeScript, Hugo, Go, Rust, Java, C/C++, mixed repositories и других проектов.

## Жёсткие правила

- Язык отчёта: русский.
- Режим: только аудит.
- Исходный код не изменять.
- Файлы проекта не форматировать.
- Автофиксы не запускать.
- Тесты, build, analyze, lint, package install не запускать.
- Разрешено только читать файлы и выполнять read-only команды.
- Разрешено создать только папку `audit_reports/` и Markdown-файл отчёта.
- Все выводы должны быть основаны на фактах из файлов, структуры проекта, git-состояния и read-only inspection.
- Если проблема не подтверждена, помечать как `Требует проверки`.
- Не показывать полные секреты, ключи, токены, пароли. Только маскированный вид.

## Файл отчёта

Создать директорию, если её нет:

```bash
mkdir -p audit_reports
```

Сохранить отчёт в формате:

```text
audit_reports/YYYY-MM-DD-audit-report.md
```

Для даты 2026-06-18 пример:

```text
audit_reports/2026-06-18-audit-report.md
```

## Разрешённые команды

Можно использовать только read-only команды:

```bash
pwd
ls
find
tree
cat
sed
head
tail
wc
du
file
grep
rg
git status --short
git branch --show-current
git log --oneline -n 20
git diff --stat
git diff --name-only
```

Можно читать файлы конфигурации, lock-файлы, документацию, исходники и тесты.

Нельзя запускать:

```bash
npm install
npm test
npm run build
pnpm install
pnpm test
yarn
flutter analyze
flutter test
flutter build
uv sync
uv run
pytest
cargo test
cargo build
go test
make
docker
```

Если для проверки нужна такая команда, записать это в раздел `Не проверено`.

## Этапы аудита

### 1. Верхний уровень репозитория

Изучить:

- корень репозитория;
- README;
- документацию;
- структуру папок;
- package/build файлы;
- lock-файлы;
- конфиги;
- CI/CD;
- scripts;
- entry points;
- тестовые папки;
- ассеты;
- generated files;
- ignored files.

Определить:

- что это за проект;
- основной стек;
- основной runtime;
- как проект должен запускаться;
- где находится главный код;
- где находятся тесты;
- какие части выглядят устаревшими, временными или сломанными.

### 2. Git-состояние

Проверить:

```bash
git status --short
git branch --show-current
git log --oneline -n 20
git diff --stat
git diff --name-only
```

В отчёте указать:

- текущую ветку;
- есть ли uncommitted changes;
- какие файлы изменены;
- есть ли подозрительные generated/cache/build files;
- какие области менялись недавно.

### 3. Стек и зависимости

Найти и изучить:

- `package.json`
- `pnpm-lock.yaml`
- `yarn.lock`
- `package-lock.json`
- `pyproject.toml`
- `uv.lock`
- `requirements.txt`
- `pubspec.yaml`
- `Cargo.toml`
- `go.mod`
- `pom.xml`
- `build.gradle`
- `CMakeLists.txt`
- `Dockerfile`
- `.github/workflows/*`
- другие build/config файлы.

Проверить:

- смешение package managers;
- отсутствие lock-файлов;
- устаревшие или дублирующиеся конфиги;
- подозрительные scripts;
- hardcoded paths;
- неочевидные environment variables;
- скрытые зависимости от локальной машины;
- несогласованность README и реальных файлов.

### 4. Архитектура

Разобрать проект на слои:

- UI / presentation;
- domain / business logic;
- data / persistence;
- API / network;
- state management;
- platform-specific layer;
- services;
- utils/helpers;
- tests;
- tooling/scripts.

Найти:

- нарушение границ слоёв;
- смешение UI и business logic;
- смешение storage/network/domain логики;
- circular dependencies;
- god objects;
- слишком большие файлы;
- дублирование логики;
- неясные ownership zones;
- мёртвые или устаревшие модули.

### 5. Runtime flow

Найти главные entry points и проследить основные потоки:

- запуск приложения;
- инициализация;
- загрузка конфигов;
- работа с данными;
- network/API calls;
- сохранение состояния;
- обработка ошибок;
- logging;
- background tasks;
- platform-specific behavior.

Для каждого важного flow указать:

- entry point;
- цепочку вызовов;
- где меняется состояние;
- где происходит I/O;
- где возможны ошибки;
- где нет обработки ошибок;
- где скрыты плохие предположения.

### 6. Тесты

Только читать тесты, не запускать.

Проверить:

- какие типы тестов есть;
- что реально покрыто;
- какие важные сценарии не покрыты;
- есть ли disabled/skipped tests;
- есть ли тесты без сильных assertions;
- есть ли тесты, завязанные на детали реализации;
- есть ли устаревшие fixtures/mocks.

### 7. Качество кода

Искать:

- dead code;
- unused files;
- duplicated code;
- long files;
- long functions;
- excessive nesting;
- inconsistent naming;
- TODO/FIXME/HACK;
- magic numbers;
- hardcoded values;
- плохую обработку ошибок;
- silent failures;
- неочевидные side effects;
- глобальное mutable state;
- плохую читаемость;
- временные решения, ставшие постоянными.

### 8. Security / privacy

Проверить:

- случайно закоммиченные ключи;
- токены;
- пароли;
- `.env`;
- credentials;
- private URLs;
- небезопасный shell execution;
- небезопасную работу с файлами;
- отсутствие input validation;
- логирование чувствительных данных;
- чрезмерные permissions.

Секреты маскировать:

```text
Возможный секрет: ABCD...WXYZ
```

### 9. Performance / resources

Искать:

- тяжёлые операции на старте;
- repeated expensive calls;
- blocking I/O;
- лишние rebuild/rerender;
- большие ассеты;
- большие бинарники;
- неограниченные коллекции;
- memory leak risks;
- лишние зависимости;
- дорогие синхронные операции.

Разделять:

- подтверждённые проблемы;
- вероятные риски;
- то, что требует runtime-проверки.

### 10. Documentation / DX

Проверить:

- README;
- setup instructions;
- команды запуска;
- environment variables;
- troubleshooting;
- архитектурную документацию;
- contribution docs;
- release process;
- scripts.

Найти:

- устаревшие инструкции;
- отсутствующие команды;
- несоответствие документации реальному проекту;
- плохой onboarding;
- скрытые знания, нужные для запуска проекта.

## Формат отчёта

Отчёт должен быть сохранён в `audit_reports/YYYY-MM-DD-audit-report.md`.

Структура:

```markdown
# Audit Report

Дата: YYYY-MM-DD
Репозиторий: <path или name>
Ветка: <branch>
Режим: read-only audit
Язык отчёта: русский

## 1. Executive Summary

Короткое резюме состояния проекта.

## 2. Severity Overview

| Severity | Count |
|---|---:|
| Critical | 0 |
| High | 0 |
| Medium | 0 |
| Low | 0 |
| Info | 0 |

## 3. Top Findings

Самые важные найденные проблемы.

## 4. Repository Map

Карта структуры проекта.

## 5. Git State

Текущая ветка, изменённые файлы, состояние рабочей копии.

## 6. Stack and Dependencies

Стек, package managers, lock-файлы, зависимости, build-конфиги.

## 7. Architecture Audit

Архитектурные слои и проблемы между ними.

## 8. Runtime Flow Audit

Главные runtime flows и найденные риски.

## 9. Test Audit

Что покрыто тестами, что не покрыто, слабые места тестов.

## 10. Code Quality Audit

Поддерживаемость, читаемость, дублирование, dead code.

## 11. Security and Privacy Audit

Секреты, небезопасные паттерны, privacy risks.

## 12. Performance Audit

Риски производительности и потребления ресурсов.

## 13. Documentation and Developer Experience

README, setup, команды, onboarding, docs.

## 14. Root Cause Analysis

Корневые причины повторяющихся проблем.

## 15. Recommended Audit-Based Fix Order

Это не реализация фиксов, а порядок, в котором стоит разбирать проблемы.

1. Critical blockers.
2. Build/runtime correctness risks.
3. Architecture boundary problems.
4. High-risk data/state bugs.
5. Missing tests.
6. Code cleanup.
7. Documentation.

## 16. Detailed Findings

### Finding 1: <title>

Severity: Critical | High | Medium | Low | Info  
Status: Confirmed | Likely | Требует проверки  
Location: `path/to/file.ext`

Проблема:

Доказательства:

Корневая причина:

Влияние:

Рекомендация:

Как проверить:

## 17. Commands Run

Список read-only команд, которые были выполнены.

## 18. Not Verified

Что не было проверено из-за read-only режима.
```

## Severity правила

### Critical

Ломает запуск, сборку, данные, безопасность или раскрывает секреты.

### High

Вероятный production bug, серьёзный runtime-риск, важный сломанный flow, плохая архитектурная связность.

### Medium

Проблемы поддержки, слабые тесты, дублирование, хрупкая логика, performance risk.

### Low

Мелкий cleanup, naming, docs, formatting, небольшие улучшения.

### Info

Нейтральное наблюдение или контекст.

## Финальный ответ пользователю

После завершения аудита ответить кратко:

```text
Аудит репозитория завершён.

Отчёт сохранён:
audit_reports/YYYY-MM-DD-audit-report.md

Главные находки:
1. ...
2. ...
3. ...
```
