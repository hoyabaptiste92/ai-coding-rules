# Copilot Usage Guidelines – Java Edition

This document provides guidance on using GitHub Copilot in this repository, which features:

- **Spring Boot backend** (Java, Maven)
- **React frontend** (Node, Next.js, Yarn)

## General Copilot Guidelines

- **Review all suggestions:** Always review Copilot’s output for accuracy, style, and security.
- **Write clear prompts:** Use descriptive comments or function signatures to get better code suggestions.
- **Avoid secrets:** Never accept suggestions with secrets, passwords, or access tokens.
- **Check dependencies:** Ensure Copilot’s suggestions use project-approved libraries only.
- **Document code:** Add Javadoc or comments to clarify Copilot-generated code.

---

## Spring Boot Backend (Java + Maven)

### 1. Code Style & Structure

- **Follow project conventions:** Use our standard code style (naming, formatting, package structure).
- **Spring Annotations:** Ensure correct use of `@RestController`, `@Service`, `@Repository`, etc.
- **Maven dependencies:** Add new dependencies to `pom.xml` only if they are necessary and approved.

### 2. Copilot Prompts

- Use detailed comments or TODOs before writing a method or class to guide Copilot.
- Example:
    ```java
    // TODO: Create a REST endpoint that returns all users as JSON
    ```
- Review and refactor Copilot’s code for:
    - Null safety
    - Security (input validation, no SQL injection)
    - Proper exception handling

### 3. Testing

- Prefer JUnit 5 for tests.
- Use MockMvc for controller testing.
- Ensure tests are added for all major Copilot-generated code.

### 4. Security

- Never accept hardcoded credentials or secrets.
- Validate all inputs in controllers and services.
- Check for SQL injection and XSS vulnerabilities.

---

## React Frontend (Node.js, Next.js, Yarn)

### 1. Code Style & Structure

- Follow our ESLint and Prettier rules.
- Use functional components and React hooks.
- Organize code by feature or domain.

### 2. Copilot Prompts

- Use clear comments to guide Copilot.
- Example:
    ```js
    // TODO: Fetch user data from the backend and display in a table
    ```
- Refactor Copilot output to match our folder structure, naming conventions, and best practices.

### 3. Testing

- Use Jest and React Testing Library.
- Add/Update tests for new Copilot-generated components or logic.

### 4. Security

- Never check in API keys or secrets.
- Sanitize user input before rendering.
- Avoid using deprecated or untrusted npm packages.

---

## Pull Requests & Review

- Clearly indicate which code was generated or heavily influenced by Copilot.
- Ask for thorough code reviews, especially for security-sensitive code.
- Remove any Copilot suggestions that do not meet project or team standards.

---

## Troubleshooting Copilot

- If Copilot produces low-quality suggestions, try rephrasing comments or writing more descriptive function signatures.
- If Copilot suggests deprecated APIs, replace them with current best practices.
- Share Copilot feedback and improvements with the team.

---

## References

- [Spring Boot Docs](https://spring.io/projects/spring-boot)
- [React Docs](https://react.dev/)
- [Next.js Docs](https://nextjs.org/docs)
- [GitHub Copilot Docs](https://docs.github.com/en/copilot)

