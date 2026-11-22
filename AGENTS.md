# AGENTS.md

`lus-lang/atmos-log` is the repository of the `log` package of the atmosphere registry. Programs load the package with `require("https://atmosp.here/2.0/log.lus")`.

## Scope

`log` writes structured log records as JSON lines, with levels, child loggers that add fields, and redaction of named fields. `log.pretty` formats the lines for a terminal. Registered on a `web` application, the package logs one line per request. The public API is every function that `log.lus` returns in its module table. A change to that API needs a new entry in `CHANGELOG.md` and a version change in the header.

## Layout

- `log.lus` is the whole package. Its header doc comment contains the package metadata and the declared permissions.
- `tests/*_test.lus` are the tests. They load `log.lus` from the parent of `TEST_DIR`, the directory that holds the test file.

The tests load `web` from a checkout of `lus-lang/atmos-web` next to this repository, so clone it into the same parent directory first.

## Commands

Run these commands from the root of the repository.

```sh
lus test tests          # run the tests
lus check log.lus     # lint, including the package codes
lus doc log.lus       # print the reference
```

## Rules

- Every public function has a doc comment that states each result and each error, following `spec/design/style.md` of the Lus repository.
- The package never calls `pledge`. A new permission is declared in the header and in the README.
- Prose follows the `lus-writing` skill, which `lus agents init` installs and https://lus.dev/agents/skills/lus-writing/SKILL.md serves. In particular, prose has no dashes or semicolons and never names the Roblox Lua dialect.
- Every bug fix comes with a test that fails without it.
