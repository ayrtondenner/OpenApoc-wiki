# Future Works

Ideas for leveraging the research and documentation produced during the AI-assisted documentation overhaul. Each item includes context from the Discord mining and wiki creation process.

## Checklist

### Code Contributions

- [ ] **Fix grenade damage values** — Our research confirmed AP Grenade should be 48 (currently 56 in OA) and HE should be 90 (currently 120). These are XML data fixes in `agent_equipment.xml`. Evidence: skin36 confirmed from disassembly that "damage, like other weapon values, are constants coded into the game."
- [ ] **Fix Advanced Security Turret beam type** — Currently uses Devastator beams instead of the correct Disrupter beams. Identified by filmboy84 (2019). Data-only fix.
- [ ] **Investigate TICKS_MULTIPLIER double-conversion** — The data extractor multiplies `fire_delay` by `TICKS_MULTIPLIER`, but `update()` already does this conversion. Causes weapon stats to be ~4x wrong (e.g., Heavy Launcher AG: OG=80, OA=320). Identified by JonnyH (Oct 2019).
- [ ] **Verify accuracy formula against codebase** — Cross-reference skin36's confirmed RSS inaccuracy model (`sqrt(agent^2 + weapon^2 + health^2 + wound^2 + berserk^2 + cloak^2)`) against the OpenApoc implementation. Create targeted PRs for discrepancies.
- [ ] **Verify fire rate formula** — Cross-reference `fire_rate = random(fire_delay) + fire_delay/2` from disassembly against OpenApoc's implementation.

### UFOpaedia Wiki Updates

- [ ] **Paste 8 MediaWiki rewrite files** — The `wiki-updates/` directory contains fully formatted MediaWiki markup ready to copy-paste into [UFOpaedia](https://www.ufopaedia.org/index.php/OpenApoc). Priority order: Compiling (has wrong dependencies), Installing, Main page, Hidden Features, Controls, Improvements, Differences, Modding (new page).

### OpenApoc Upstream

- [ ] **Propose wiki submodule to upstream** — Open a PR to [OpenApoc/OpenApoc](https://github.com/OpenApoc/OpenApoc) proposing to add this wiki as a submodule. The upstream wiki (`OpenApoc/OpenApoc.wiki.git`) only has 4 pages; ours has 30+.
- [ ] **Create GitHub Issues from findings** — Turn confirmed data errors and missing implementations into actionable GitHub issues with Discord evidence.

### Tooling

- [ ] **Build a Discord knowledge search tool** — Create a script (Python or Node) to search the 121 MB of JSON exports by keyword, author, date range, or channel. Alternatively, create an MCP server exposing Discord search for future Claude sessions.

### Documentation

- [ ] **Create a developer onboarding guide** — Write `wiki/development/getting-started.md` covering: first PR walkthrough, key files, common pitfalls (StateRef, TPS assumptions, clang-format), serialization system, State/UI boundary.
- [ ] **Create a modding tutorial** — The #mod_development Discord mining revealed a complete step-by-step workflow for adding weapons, modifying XML, and creating sprites. Turn this into a proper tutorial with examples.
- [x] **Write "State of OpenApoc 2026"** — Comprehensive project status document compiled from all research. See [State of OpenApoc 2026](state-of-openapoc-2026.md).
- [x] **Update Claude auto-memory** — Reference the wiki submodule, key findings, Discord exports location, and critical formulas in the Claude Code memory file for future sessions.

## See Also

- [Research Statistics](research-stats.md) — Metrics of the documentation overhaul
- [Discord Mining Summary](mining-summary.md) — All 20 critical findings from Discord
- [State of OpenApoc 2026](state-of-openapoc-2026.md) — Project status assessment
