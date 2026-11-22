# log

Writes structured log records as JSON lines, with levels, child loggers that add fields, and redaction of named fields. A pretty printer formats the lines for a terminal. A `web` plugin logs one line per request.

```lus nocheck
local log = require("https://atmosp.here/2.0/log.lus")

local logger = log.new({ level = "info", redact = { "password", "user.token" } })
local db_log = logger:child({ component = "db" })
db_log:info("connected", { host = "localhost", ms = 12 })
--> {"level":"info","time":1782998100250,"component":"db","msg":"connected","host":"localhost","ms":12}

app:register(log, { logger = logger })
```

The package requires Lus 2.0. It needs no permissions. It calls no `pledge` of its own, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `log.lus`. Run `lus doc log.lus` to print it.

`lus bench/micro.lus` measures the cost of a call. A call at a disabled level costs the same as a call of an empty method, a few nanoseconds. A call at an enabled level costs one `tojson` call for the fields, one reading of the clock, and one write.
