# Changelog

All notable changes to the `reverse-todo` skill.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versions follow [SemVer](https://semver.org/).

---

## [1.1.0] - 2026-05-27

### Added

- **Obsidian sync.** After every local write, the same file mirrors to `~/Documents/Obsidian Vault/Reverse To-Do/YYYY-MM-DD.md` with Obsidian-friendly frontmatter additions (`tags: [reverse-todo, daily-log]`, `cssclass: reverse-todo`). Reviews go to `reviews/` subfolder.
- **Notion sync.** One page per day in a "Reverse To-Do List" database. Properties: Name, Date, Total Score, Entry Count, 6 category numbers, Has Recap. Reviews go as child pages under the parent (not inside the day-database) titled "Week of YYYY-MM-DD" or "Month of YYYY-MM".
- **First-log Notion setup flow.** When `sync.notion.database_id` is null, the skill prompts the user to pick a parent page from their workspace, creates the database with the full schema, and persists the resulting IDs to `config.json` so it never has to ask again.
- **`sync` block in `config.json`** with per-target `enabled` toggles, vault path, and Notion IDs.
- **`references/sync-obsidian.md`** documenting the vault write rules and failure handling.
- **`references/sync-notion.md`** documenting the Notion MCP tool calls, property schema, and the search-and-upsert logic.
- **README.md** in the skill's voice, ADHD-focused, with the full how-to.
- **CHANGELOG.md** (this file).

### Changed

- **SKILL.md** now runs a Sync step after every local write in log, recap, and review modes. Local markdown is the source of truth; Obsidian and Notion are mirrors.
- Recap mode flips the Notion `Has Recap` checkbox to true on write.

### Notes

- **Failure handling:** if a sync target fails (vault missing, Notion offline, MCP not connected), the skill skips that target silently, mentions it ONCE in the next confirmation, and never blocks the local log. Local always writes. Local always wins.
- **Source of truth:** local markdown at `~/reverse-todo/YYYY/MM/YYYY-MM-DD.md` is canonical. Obsidian and Notion are write-only mirrors. If you want to edit, edit the local file (or any of the three) and re-run a log to re-sync everything.

---

## [1.0.0] - 2026-05-27

Initial release. ADHD-friendly reverse to-do list with 0-100 effort scoring and best-friend voice.

### Added

- **Three modes:** `log` (default), `recap`, `review` (week/month).
- **Six categories** designed to make ADHD brains feel seen instead of judged:
  - Small Tasks
  - Self-Care
  - Emotional Stuffs
  - Big Brain Hours
  - Creative Time
  - Rest (treated as output, not absence of output)
- **0-100 effort scoring per entry** with a rubric in `references/scoring.md`. 100 = a full day's worth of human output. Includes bad-day multiplier (x1.5-2), invisible labor multiplier (x1.3-1.5), ADHD executive function tax (+5 to +15), and first-time-in-a-while multiplier (x1.5).
- **Over-100 brain-lying call-out** in recap mode. When the total crosses 100, the recap explicitly tells the user their brain is about to try to discount it and not to let it.
- **Best-friend voice** codified in `references/voice.md`. Calls out self-sabotage, swears where it lands, bans productivity-bro language, treats rest as real work, names invisible labor explicitly.
- **Pattern-only reviews** in `references/review-template.md`. Surfaces specific day-of-week / category / score-trend patterns, skips generic stats.
- **Local markdown storage** at `~/reverse-todo/YYYY/MM/YYYY-MM-DD.md`. Plain text, greppable, portable.
- **Capitalization rules** added late on launch day after the user noticed all-lowercase entries. Voice is casual, not aesthetically lowercase. Proper sentence case everywhere.
- **No em-dashes, no en-dashes** as a hard rule across all output.

### Known limitations

- Single-day, single-user. No multi-day batch logging from a transcript yet.
- No manual score override in v1 (auto-only). Hybrid mode is on the roadmap if scores feel off.
- No body / cycle awareness tagging (intentionally deferred).
- No win archive / bad-day comparison / crash prediction yet (queued for v3 / v4).

---

[1.1.0]: #110---2026-05-27
[1.0.0]: #100---2026-05-27
