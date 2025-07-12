# Copilot Code Guidelines for C#/.NET 9.0

## Implementation Best Practices

### 0 — Purpose

These rules ensure maintainability, safety, and developer velocity.  
**MUST** rules are enforced by CI; **SHOULD** rules are strongly recommended.

---

### 1 — Before Coding

- **BP-1 (MUST)** Ask the user clarifying questions about requirements and edge cases.
- **BP-2 (SHOULD)** Draft and confirm an approach for complex work (e.g., diagram, pseudocode, or summary).
- **BP-3 (SHOULD)** If ≥ 2 approaches exist, list clear pros and cons.

---

### 2 — While Coding

- **C-1 (MUST)** Use Test-Driven Development (TDD): write a failing unit test → implement code → refactor.
- **C-2 (MUST)** Name methods and variables using established domain vocabulary and .NET naming conventions (PascalCase for methods/classes, camelCase for locals/parameters).
- **C-3 (SHOULD NOT)** Introduce classes or interfaces if small, testable methods suffice.
- **C-4 (SHOULD)** Prefer simple, composable, testable methods.
- **C-5 (MUST)** Prefer strong (typed) identifiers over using `string` or `int` for domain IDs.
  ```csharp
  // ✅ Good
  public readonly record struct UserId(Guid Value);

  // ❌ Bad
  public string UserId;
  ```
- **C-6 (MUST)** Use explicit types for dependencies and avoid dynamic or object unless necessary.
- **C-7 (SHOULD NOT)** Add comments except for critical caveats; rely on self-explanatory code and meaningful names.
- **C-8 (SHOULD)** Favor records, structs, or classes as appropriate; use interfaces when needed for abstraction or testability.
- **C-9 (SHOULD NOT)** Extract a new method unless it will be reused, enhances testability, or drastically improves clarity.

---

### 3 — Testing

- **T-1 (MUST)** Colocate unit tests in `*.Tests.cs` files in the same directory as the code under test.
- **T-2 (MUST)** For any public API change, add/extend integration tests in the appropriate test project.
- **T-3 (MUST)** Separate pure logic unit tests from integration tests (e.g., those that touch a database or external system).
- **T-4 (SHOULD)** Prefer integration tests over heavy mocking when possible.
- **T-5 (SHOULD)** Unit-test complex algorithms thoroughly.
- **T-6 (SHOULD)** Assert on the full result object, not only on individual properties, when practical.
  ```csharp
  // Good
  Assert.Equal(expected, actual);

  // Bad
  Assert.Equal(expected.Count, actual.Count);
  Assert.Equal(expected.Item1, actual.Item1);
  ```

---

### 4 — Database

- **D-1 (MUST)** Explicitly type database helpers (e.g., `DbContext`, `IDbConnection`).
- **D-2 (SHOULD)** Override or wrap incorrect generated types if needed (e.g., for GUIDs, enums, BigInteger).

---

### 5 — Code Organization

- **O-1 (MUST)** Place code in a shared project or library only if it is used by ≥ 2 projects.

---

### 6 — Tooling Gates

- **G-1 (MUST)** `dotnet format` passes (style and formatting).
- **G-2 (MUST)** `dotnet build`, `dotnet test`, and `dotnet analyzers` pass without warnings or errors.

---

### 7 — Git

- **GH-1 (MUST)** Use Conventional Commits format for commit messages: https://www.conventionalcommits.org/en/v1.0.0
- **GH-2 (SHOULD NOT)** Refer to Copilot, OpenAI, or Anthropic in commit messages.

---

## Writing Methods Best Practices

When evaluating a method you implemented, use this checklist:

1. Can you read the method and easily follow what it's doing?
2. Does the method have high cyclomatic complexity? (e.g., deeply nested if/else) If so, refactor.
3. Are there standard .NET collections or algorithms that would make this easier to follow or more robust?
4. Are there any unused parameters?
5. Are there unnecessary casts that can be moved to the method signature?
6. Is the method easily testable without mocking core features (e.g., EF Core, HTTP clients)? If not, can you test it as part of an integration test?
7. Does it have hidden dependencies or values that should be arguments instead?
8. Brainstorm 3 better method names and see if the current name is the best and consistent with the codebase.

**IMPORTANT:**  
DO NOT refactor out a separate method unless:
- The new method is used in more than one place.
- It is more easily unit tested when separated.
- The original method is so hard to follow that comments would otherwise be required.

---

## Writing Tests Best Practices

When evaluating a test you've implemented, use this checklist:

1. SHOULD parameterize inputs; avoid unexplained literals (e.g., 42, "foo").
2. SHOULD NOT add trivial tests that cannot fail for a real defect (e.g., Assert.Equal(2, 2)).
3. SHOULD ensure the test name and assertion align (rename or rewrite if not).
4. SHOULD compare results to independent, pre-computed expectations or domain properties, never to the function’s output reused as an oracle.
5. SHOULD follow the same lint, type-safety, and style rules as production code.
6. SHOULD express invariants or properties (e.g., commutativity, idempotence, round-trip) when practical, using property-based testing libraries (e.g., FsCheck, Xunit.Theories).
   ```csharp
   [Property]
   public void StringConcat_Length(string a, string b)
   {
       Assert.Equal((a + b).Length, a.Length + b.Length);
   }
   ```
7. Unit tests for a method should be grouped under a single test class or fixture.
8. Use `Assert.IsType<T>(...)` or `Assert.Any(...)` where appropriate for variable values.
9. ALWAYS use strong assertions (e.g., `Assert.Equal(x, 1)`) over weaker ones (e.g., `Assert.True(x >= 1)`).
10. SHOULD test edge cases, realistic input, unexpected input, and value boundaries.
11. SHOULD NOT test conditions enforced by the type checker.

---

## Code Organization

- `Api/` - ASP.NET Core API project
- `Web/` - Blazor or ASP.NET Core MVC/Razor app
- `Shared/` - Shared types and utilities (.NET class library)
- `Data/` - Data access logic and models

---

## Remember Shortcuts

### QNEW

When I type "qnew", this means:
```
Understand all BEST PRACTICES listed in this document.
Your code SHOULD ALWAYS follow these best practices.
```

### QPLAN

When I type "qplan", this means:
```
Analyze similar parts of the codebase and determine whether your plan:
- is consistent with rest of codebase
- introduces minimal changes
- reuses existing code
```

### QCODE

When I type "qcode", this means:
```
Implement your plan and make sure new tests pass.
Always run tests to make sure nothing else breaks.
Always run `dotnet format` on newly created files.
Always run `dotnet build` and `dotnet analyzers` to ensure type checking and linting passes.
```

### QCHECK

When I type "qcheck", this means:
```
You are a SKEPTICAL senior engineer.
For every MAJOR code change (skip minor changes):
1. Apply the Writing Methods Best Practices checklist.
2. Apply the Writing Tests Best Practices checklist.
3. Apply the Implementation Best Practices checklist.
```

### QCHECKF

When I type "qcheckf", this means:
```
You are a SKEPTICAL senior engineer.
For every MAJOR method you added or edited (skip minor changes):
1. Apply the Writing Methods Best Practices checklist.
```

### QCHECKT

When I type "qcheckt", this means:
```
You are a SKEPTICAL senior engineer.
For every MAJOR test you added or edited (skip minor changes):
1. Apply the Writing Tests Best Practices checklist.
```

### QUX

When I type "qux", this means:
```
Imagine you are a human UX tester of the feature you implemented. 
Output a comprehensive list of scenarios you would test, sorted by highest priority.
```

### QGIT

When I type "qgit", this means:
```
Add all changes to staging, create a commit, and push to remote.

Commit message checklist:
- Use Conventional Commits format: https://www.conventionalcommits.org/en/v1.0.0
- Do NOT refer to Copilot, OpenAI, or Anthropic in the commit message.
- Structure:
    <type>[optional scope]: <description>
    [optional body]
    [optional footer(s)]
- Indicate intent: fix: (bug), feat: (feature), BREAKING CHANGE: (major change), or others as needed.
```

---

This guideline is tailored for C#/.NET 9.0 projects using GitHub Copilot. You may further customize code examples and directory names as your solution evolves