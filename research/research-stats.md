# Research Statistics

Metrics and scale of the AI-assisted documentation overhaul that produced this wiki and its Discord-mined community knowledge.

**AI Tooling**: [Claude Opus 4.6](https://docs.anthropic.com/en/docs/about-claude/models) (1M context window) running via [Claude Code](https://docs.anthropic.com/en/docs/claude-code) on VSCode.

## Session Duration

- **~5 hours 42 minutes** in a single continuous session (6:30 PM to 12:12 AM)
- **17-step master plan** designed, approved, and executed from start to finish
- **~13 parallel AI agents** launched across the project for concurrent research and writing

---

## Discord Knowledge Mining

The OpenApoc Discord server was mined using MCP integration and extraction tools to process 8+ years of community discussions.

| Metric | Value |
|--------|-------|
| **Total Discord messages read** | **77,612** |
| **JSON data processed** | **121 MB** (3,863,352 lines of JSON) |
| **Channels exported** | **25** (10 more were archived/restricted) |
| **Pinned messages analyzed** | **95** |
| **Unique message authors** | **3,352** |
| **Years of history covered** | **~8.3 years** (November 2017 — February 2026) |
| **Largest single channel** | `general_openapoc` — **28,176 messages**, 45 MB |
| **Mining agents** | 5 parallel agents processed the top channels simultaneously |

The full extraction results are documented in the [Discord Mining Summary](mining-summary.md).

---

## Documentation Written

| Output | Files | Lines |
|--------|-------|-------|
| Wiki markdown files (GitHub repo) | **27 files** | **6,044 lines** |
| MediaWiki files (for UFOpaedia paste) | **8 files** | **2,143 lines** |
| Discord-mined additions (enrichment pass) | **13 files updated** | **+1,001 lines** |
| Mining summary | 1 file | 169 lines |
| **Total** | **36 files** | **~8,356 lines** |

---

## UFOpaedia Wiki Audit

| Metric | Value |
|--------|-------|
| **Pages audited** | **11** (all OpenApoc pages on UFOpaedia) |
| **Pages with proposed rewrites** | **8** (Compiling, Installing, Main, Hidden Features, Controls, Improvements, Differences, Modding) |
| **New page proposed** | **1** (Modding — zero wiki documentation previously existed) |
| **Highest priority fix** | Compiling page — had **factually wrong dependencies** that would cause build failures for anyone following it |

---

## Codebase Research

| Metric | Value |
|--------|-------|
| **Key source files analyzed** | `framework/options.cpp` (54+ options), `README_HOTKEYS.txt` (197 lines), `README.md`, `CODE_STYLE.md`, `vcpkg.json`, `CMakeLists.txt`, `tools/extractors/docs/*` |
| **GitHub PRs reviewed** | **50+** recent PRs analyzed for feature and decision context |
| **GitHub milestones examined** | **4** (Alpha #263, Beta #264, 1.0 #265, Extra Features #941) |
| **Roadmap issues analyzed** | Hundreds of issues across all milestones |

---

## Internet Research

| Metric | Value |
|--------|-------|
| **Web searches performed** | **20+** queries across game guides, UFOpaedia, StrategyWiki, GameFAQs |
| **Pages fetched and analyzed** | **15+** web pages for original game mechanics and tooling |
| **Key references discovered** | Wong's 1997 FAQ, Terry Greer's artist page, Thaddaeus Frogley's developer portfolio, Ghidra LX loader |

---

## Knowledge Extracted

| Discovery Category | Count |
|-------------------|-------|
| **Game formulas confirmed from disassembly** | **4** (accuracy RSS, fire rate, transport generation, AI evaluation) |
| **Cut features documented** | **15+** (procedural dimensions, tracker gun, VIP system, sonic weapons, and more) |
| **Original game bugs discovered** | **10+** (GOG executables, Learning AI save/load, midnight freeze, and more) |
| **OpenApoc vs OG differences found** | **11** new differences (explosion radius, grenade damage, tick rate, and more) |
| **Architecture insights** | **7** major findings (StateRef, TPS #997, serialization, ECS proposal, and more) |
| **Modding system details** | **13** subsections of new modding knowledge |
| **Key contributors profiled** | **10** core developers and researchers |

---

## Infrastructure Created

| Item | Details |
|------|---------|
| **GitHub wiki repo** | [ayrtondenner/OpenApoc-wiki](https://github.com/ayrtondenner/OpenApoc-wiki) — 27+ files, added as git submodule |
| **Discord server export** | Full channel export of OpenApoc Discord via MCP and extraction tools |
| **8 UFOpaedia rewrite files** | Ready-to-paste MediaWiki markup in `wiki-updates/` |

---

## Most Remarkable Finding

**Julian Gollop** (the creator of X-COM) **personally confirmed** that X-COM: Apocalypse uses a **neural network** (6-layer multilayer perceptron) for its tactical AI — a fact that was largely unknown to the wider gaming community and only surfaced through persistent questioning by community member Bluddy on the OpenApoc Discord.

---

## See Also

- [Discord Mining Summary](mining-summary.md) — Full catalog of all 20 critical findings extracted from Discord
- [Architecture](../development/architecture.md) — Technical architecture insights from Discord mining
- [Roadmap](../openapoc/roadmap.md) — Development status enriched with community findings
