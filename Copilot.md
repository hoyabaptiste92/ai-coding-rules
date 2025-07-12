# Copilot and AI Coding Assistant Guidelines for .NET and C#

## Why These Guidelines?
AI coding assistants like GitHub Copilot can dramatically speed up software development. However, they may introduce subtle errors, use outdated APIs, or miss organizational standards. These guidelines ensure safe, maintainable, and high-quality .NET/C# code when using AI tools.

---

## Table of Contents
1. [Principles](#principles)
2. [Best Practices Checklist](#best-practices-checklist)
3. [Security Guidelines](#security-guidelines)
4. [Accessibility & Globalization](#accessibility--globalization)
5. [AI-Generated Code Review](#ai-generated-code-review)
6. [Commits & Messaging](#commits--messaging)
7. [Workflow Shortcuts](#workflow-shortcuts)
8. [Common Pitfalls](#common-pitfalls)
9. [Further Reading](#further-reading)

---

## Principles

| Rule Type | Meaning                                 |
|-----------|-----------------------------------------|
| MUST      | Required—never skip                     |
| SHOULD    | Strongly recommended—exceptions rare    |
| SHOULD NOT| Strongly discouraged—exceptions rare    |
| MAY       | Optional—use your judgment              |

---

## Best Practices Checklist

### Naming and Structure
- **MUST** use [Microsoft C# naming conventions](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines).
- **MUST** prefer explicit types over `var` unless type is obvious from the right-hand side.
- **SHOULD** use strong domain identifiers, e.g., `record struct OrderId(Guid Value);`.
- **SHOULD** group related code, keeping tests close to source files.

### Design and Readability
- **MUST** prioritize clarity and simplicity over cleverness.
- **SHOULD** write small, composable methods; avoid deep nesting.
- **SHOULD** remove redundant comments; code should be self-explanatory.
- **SHOULD** minimize unnecessary abstractions.

### Testing
- **MUST** practice Test-Driven Development (TDD) where practical.
- **SHOULD** colocate unit tests with implementation.
- **SHOULD** separate integration tests from unit tests.
- **SHOULD** use property-based testing for core logic.

### Automation and Quality
- **MUST** pass `dotnet build`, `dotnet format`, and static analysis before merging.
- **SHOULD** use code analyzers and security linters.

**Quick Reference Table**

| Practice                                     | MUST/SHOULD | Notes                        |
|-----------------------------------------------|-------------|------------------------------|
| C# Naming Conventions                        | MUST        |                              |
| Explicit Types                               | MUST        | Use `var` only when obvious  |
| Strong Domain Identifiers                    | SHOULD      |                              |
| Small/Composed Methods                       | SHOULD      |                              |
| Colocated Unit Tests                         | SHOULD      |                              |
| Separate Integration Tests                   | SHOULD      |                              |
| Code Analyzers and Linters                   | SHOULD      |                              |
| Pass Build and Format Before Merge           | MUST        |                              |

---

## Security Guidelines

- **MUST** NEVER commit secrets, API keys, or credentials.
- **SHOULD** validate all user inputs and handle errors gracefully.
- **SHOULD** review Copilot/AI code for security vulnerabilities and outdated APIs.
- **SHOULD** avoid copying license-restricted code from Copilot suggestions.
- **MUST** ensure all dependencies are up to date and free of known vulnerabilities.

---

## Accessibility & Globalization

- **SHOULD** follow [accessibility (a11y)](https://learn.microsoft.com/en-us/accessibility/dev-guide/) guidelines for UI code.
- **SHOULD** use resource files for localizable strings.
- **SHOULD** avoid hard-coding culture- or language-specific logic.

---

## AI-Generated Code Review

- **MUST** NEVER merge AI-generated code without human review.
- **MUST** double-check business logic, edge cases, and security aspects.
- **SHOULD** flag suspicious or unexplained code for team discussion.
- **SHOULD** verify code is compatible with project style and standards.

---

## Commits & Messaging

- **MUST** use [Conventional Commits](https://www.conventionalcommits.org/):
  - **feat**: New features
  - **fix**: Bug fixes
  - **docs**: Documentation changes
  - **test**: Adding or updating tests
  - **chore**: Maintenance tasks

**Good Example:**  
```
feat(order): add OrderId value object and validation
```

**Bad Example:**  
```
Update stuff
```

---

## Workflow Shortcuts

| Shortcut | When to Use                   | Example Usage                                     |
|----------|-------------------------------|---------------------------------------------------|
| QNEW     | New idea/feature proposal     | `QNEW: Add multi-tenancy support`                 |
| QPLAN    | Outline planned changes       | `QPLAN: Refactor payment gateway integration`     |
| QTEST    | Document test plan/results    | `QTEST: Unit tests for OrderService`              |
| QREVIEW  | Request focused code review   | `QREVIEW: Please check null handling in X`        |
| QFIX     | Quick bug fix                 | `QFIX: Corrected null reference in Y`             |

---

## Common Pitfalls

- Trusting Copilot code without reviewing for null handling, error checking, and edge cases.
- Accepting outdated APIs or deprecated patterns.
- Missing security checks on input or external data.
- Overusing `var` or generic types, harming readability.
- Merging AI-generated code without understanding it.

---

## Further Reading

- [Microsoft C# Coding Conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)
- [.NET Design Guidelines](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/)
- [OWASP Top 10 Security Risks](https://owasp.org/www-project-top-ten/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Accessibility for Developers](https://learn.microsoft.com/en-us/accessibility/dev-guide/)

---

**Remember:**  
AI coding assistants are powerful tools, but human expertise and review remain essential for safe, high-quality software.

