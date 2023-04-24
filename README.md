# heroku-buildpack-bun

Heroku buildpack for Bun.js

Largely copied from https://github.com/chibat/heroku-buildpack-deno

Pin a certain Bun version with a `runtime.bun.txt` or `runtime.txt` with e.g. `v0.5.9` in it.

Be aware that Heroku doesn't use a new enough version of the Linux kernel to support `io_uring`, which is needed for `Bun.write()`. Use `node:fs.writeFile()` instead.