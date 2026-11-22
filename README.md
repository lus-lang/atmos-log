# log

`log` writes structured log records as JSON lines, with levels, child loggers that add fields, and redaction of named fields. `log.pretty` formats the lines for a terminal. Registered on a `web` application, the package logs one line per request.

The following example sets up the logging of a web application and redacts passwords and tokens from its records.

```lus nocheck
local log = require("https://atmosp.here/2.0/log.lus")

local logger = log.new({ level = "info", redact = { "password", "user.token" } })
local db_log = logger:child({ component = "db" })
db_log:info("connected", { host = "localhost", ms = 12 })
--> {"level":"info","time":1782998100250,"component":"db","msg":"connected","host":"localhost","ms":12}

app:register(log, { logger = logger })
```

The package requires Lus 2.0 and declares no permissions. It never calls `pledge`, so the program that loads it keeps control of its permissions.

The reference is in the doc comments of `log.lus`, which `lus doc log.lus` prints.

`lus bench/micro.lus` measures the cost of a call. A call at a disabled level costs the same as a call of an empty method. A call at an enabled level costs one `tojson` call for the fields, one reading of the clock, and one write.
