# Coding Style Summary

This page summarizes the OpenApoc coding style conventions. For the complete specification, see [`CODE_STYLE.md`](https://github.com/OpenApoc/OpenApoc/blob/master/CODE_STYLE.md) in the repository root.

Code formatting is enforced by **clang-format-18** and static analysis by **clang-tidy-18**. The CI pipeline rejects unformatted code.

## Language and Tooling

- **C++17** standard
- **clang-format-18** for automatic formatting
- **clang-tidy-18** for static analysis and linting
- Always run `clang-format -i` on modified files before committing

## Formatting Rules

- **Indentation**: Tabs for indentation, spaces for alignment.
- **Column limit**: 100 characters (tab width = 4).
- **Braces**: Allman style -- opening brace on its own line.
- **Always use braces**, even for single-statement `if`/`for`/`while` blocks.
- **Namespace content is not indented**. Closing brace gets a `// namespace Name` comment.
- **Pointers and references**: Align right (`int *ptr`, `Type &ref`).
- **Line breaks**: Break before operators when wrapping; indent continuation by one extra tab.

Example:

```cpp
namespace OpenApoc
{

class MyClass
{
private:
	int memberVariable = 0;
public:
	void doSomething();
};

} // namespace OpenApoc
```

## Naming Conventions

| Style | Used For |
|-------|----------|
| `CamelCase` | Classes, enums, enum class members, namespaces, template parameters |
| `camelBack` | Methods, member variables, function parameters, local variables |
| `SHOUTY_CAPS` | Constants, macros |
| `lower_case` | Labels |

## Class Conventions

- `public:`/`private:`/`protected:` written at class indent level (not indented further).
- Always explicitly write `private:`, even though it is the default.
- `virtual` only on the base class declaration; `override` on derived classes -- never both together.
- All classes with virtual methods must have a virtual destructor.
- Use `= default` instead of empty `{}` constructor/destructor bodies.
- Use member initializer lists; initializer order must match declaration order.
- Use `struct` only for data-only types; structs must never use access modifiers.

## Project-Specific Types

### Strings

Use `UString` (from `library/strings.h`) for all strings. All `char*`/`std::string` values are assumed UTF-8.

```cpp
#include "library/strings.h"

UString name = "Phoenix Hovercar";
```

### Smart Pointers (library/sp.h)

```cpp
#include "library/sp.h"

sp<T>               // std::shared_ptr<T>
up<T>               // std::unique_ptr<T>
wp<T>               // std::weak_ptr<T>
mksp<T>(args...)    // std::make_shared<T>(args...)
mkup<T>(args...)    // std::make_unique<T>(args...)
```

Prefer `up<>` (exclusive ownership) over `sp<>` unless shared ownership is genuinely needed. Use `std::move()` to transfer `up<>` ownership. No naked `new` -- always wrap in smart pointers immediately.

### Logging (framework/logger.h)

Uses **fmt-style format strings** with positional `{0}`, `{1}`, etc. placeholders (not printf-style):

```cpp
#include "framework/logger.h"

LogInfo("Loaded mod \"{0}\"", modName);
LogWarning("Value {0} exceeds limit {1}", value, limit);
LogError("Failed to load file \"{0}\"", path);
```

- `LogInfo` -- general information
- `LogWarning` -- recoverable errors
- `LogError` -- fatal errors

### String Formatting (library/strings_format.h)

```cpp
#include "library/strings_format.h"

UString result = OpenApoc::format("Player has {0} credits and {1} agents", credits, agentCount);
```

### Translation

```cpp
UString translated = tr("English text to translate");
```

## Include and Header Conventions

- Use `#pragma once` (no traditional include guards).
- **Include order**: Local headers first, then system headers. Each block alphabetically sorted.
- **Local headers use paths relative to the OpenApoc root**: `"framework/logger.h"`, not `"../logger.h"`.
- **Prefer forward declarations** over `#include` in headers where possible.

```cpp
#pragma once

#include "library/sp.h"
#include "library/strings.h"

#include <vector>

namespace OpenApoc
{

class ForwardDeclaredType;

class MyClass
{
private:
	int member = 0;
public:
	void publicFunction();
};

} // namespace OpenApoc
```

## General Best Practices

- **Use `auto`** liberally, especially when the type is obvious from the right-hand side. Use `auto &` to avoid copies.
- **`const` aggressively**: const member functions, const parameters, const return types, const local variables.
- **Early return** is encouraged -- prefer separate `if (cond) return;` checks over deeply nested conditionals.
- **Range-for loops**: `for (auto &element : container)` or `for (const auto &element : container)`.
- **No C-style casts** -- use `static_cast<>`, `dynamic_cast<>`, `reinterpret_cast<>`.
- **Prefer `{}` brace initialization**.
- **Prefer `emplace()` over `insert()`** in STL containers.
- **Use `enum class`** over plain `enum`.
- **Use anonymous namespaces** instead of `static` for file-local functions and classes.

```cpp
namespace
{
void helperFunction()
{
	// file-local helper
}
} // anonymous namespace
```

## All Project Code Lives in namespace OpenApoc

```cpp
namespace OpenApoc
{

// All code here -- namespace content is NOT indented

} // namespace OpenApoc
```

## Key Review Expectations

These patterns are consistently enforced during code review:

1. **const correctness** -- if something can be const, it must be const.
2. **Readable conditionals** -- avoid embedded comments in complex conditionals; prefer early-exit checks.
3. **One logical change per PR** -- keep changes focused for clean history and bisectability.
4. **Use `auto`** -- when the type is already visible on the RHS.
5. **Prefer exclusive ownership** -- use `up<>` over `sp<>` when shared ownership is not required.

## Formatting Commands

```sh
# Format all source files (from build directory)
cmake --build build -t format-sources

# Format specific files
clang-format -i path/to/file.cpp path/to/file.h

# Run static analysis (from build directory)
cmake --build build -t tidy
```

## See Also

- [`CODE_STYLE.md`](https://github.com/OpenApoc/OpenApoc/blob/master/CODE_STYLE.md) -- full coding style specification
- [Architecture](architecture.md) -- codebase structure overview
- [Building](building.md) -- build instructions
