# Contributing

Run the tests with `lus test tests` from the root of the repository. The tests load `web` from a checkout of `lus-lang/atmos-web` in the same parent directory, so clone it there first.

Run `lus bench/micro.lus` to measure the cost of a call. A call at a disabled level costs the same as a call of an empty method. A call at an enabled level costs one `tojson` call for the fields, one reading of the clock, and one write.
