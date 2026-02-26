# Contributing to the OpenApoc Wiki

Thank you for your interest in improving the OpenApoc documentation!

## How to Contribute

1. **Fork** this repository
2. **Create a branch** for your changes
3. **Make your edits** following the guidelines below
4. **Submit a pull request** with a clear description of what you changed and why

## File Organization

- `original-game/` — Original X-COM: Apocalypse mechanics (reference for developers)
- `openapoc/` — OpenApoc-specific features and additions
- `comparison/` — Side-by-side comparisons (original vs OpenApoc)
- `development/` — Developer documentation (building, architecture, coding style)
- `resources/` — External links and references

## Writing Guidelines

- Use standard GitHub-flavored Markdown
- Use tables for structured data (stats, options, key bindings)
- Include a "Sources" section at the bottom of game mechanics pages, linking to [UFOpaedia](https://www.ufopaedia.org/index.php) where applicable
- Keep language clear and concise
- Prefer factual, verifiable information over speculation
- When documenting game mechanics, cite your sources (original game testing, codebase, UFOpaedia, community research)

## Verifying Information

- **Original game mechanics**: Cross-reference with [UFOpaedia](https://www.ufopaedia.org/index.php?title=Apocalypse) and the extractor docs in `tools/extractors/docs/`
- **OpenApoc features**: Verify against the actual codebase, especially `framework/options.cpp` for configurable options
- **Controls**: The source of truth is `README_HOTKEYS.txt` in the main OpenApoc repo

## Reporting Issues

If you find incorrect information but aren't sure how to fix it, please open an issue describing what's wrong and where you found the correct information.

## Related Resources

- [OpenApoc main repository](https://github.com/OpenApoc/OpenApoc)
- [UFOpaedia — OpenApoc](https://www.ufopaedia.org/index.php/OpenApoc)
- [OpenApoc Discord](https://discord.gg/f8Rayre)
