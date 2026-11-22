# AGENTS.md

This repository, `lus-lang/atmos-log`, is the `log` package of the atmosphere registry. Programs load it with `require("https://atmosp.here/2.0/log.lus")`.

## Scope

Writes structured log records as JSON lines, with levels, child loggers that add fields, and redaction of named fields. A pretty printer formats the lines for a terminal. A `web` plugin logs one line per request. The public API is every function that `log.lus` returns in its module table. A change to that API needs a new entry in `CHANGELOG.md` and a version change in the header.

## Layout

- `log.lus` is the whole package. Its header doc comment carries the package metadata and the declared permissions.
- `tests/*_test.lus` are the tests. They load the package from the parent directory through `TEST_DIR`.

The tests load `web` from a checkout of `lus-lang/atmos-web` next to this repository, so clone it into the same parent directory first.

## Commands

```sh
lus test tests          # run the tests
lus check log.lus     # lint, including the package codes
lus doc log.lus       # print the reference
```

## Rules

- Every public function has a doc comment that states each result and each error, following `spec/design/style.md` of the Lus repository.
- The package never calls `pledge`. A new permission is declared in the header and in the README.
- Prose has no dashes and no semicolons, and never names the Roblox Lua dialect.
- Every bug fix comes with a test that fails without it.
