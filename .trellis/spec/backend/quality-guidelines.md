# Quality Guidelines

> Code quality standards for backend development.

---

## Overview

<!--
Document your project's quality standards here.

Questions to answer:
- What patterns are forbidden?
- What linting rules do you enforce?
- What are your testing requirements?
- What code review standards apply?
-->

(To be filled by the team)

---

## Forbidden Patterns

<!-- Patterns that should never be used and why -->

(To be filled by the team)

---

## Required Patterns

### Proxy Type Additions

When adding a new `ProxyType`, update every boundary that carries proxy type data:

- `src/parser/config/proxy.h`: enum value, `getProxyTypeName`, shared fields, and default group macro.
- `src/parser/subparser.cpp` / `.h`: constructor and parser branch for any supported input format.
- `src/generator/config/subexport.cpp`: output branch for each supported target plus the `!!TYPE=` matcher map.
- `src/script/script_quickjs.h`: QuickJS `Proxy` wrap/unwrap fields when the new type adds fields that scripts may inspect or modify.

Good case: a Mihomo-only protocol is parsed from `explodeClash`, stored in `Proxy`, emitted from `proxyToClash`, and left unsupported in unrelated target exporters unless the task explicitly asks for those targets.

Bad case: adding only the Clash output branch. That can generate hand-created nodes, but imported subscriptions still parse as `Unknown` or lose protocol-specific fields during script processing.

---

## Testing Requirements

<!-- What level of testing is expected -->

(To be filled by the team)

---

## Code Review Checklist

<!-- What reviewers should check -->

(To be filled by the team)
