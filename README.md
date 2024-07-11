# heroku-buildpack-bun

Heroku buildpack for [Bun.js](https://bun.sh/) - allows you to run Bun on Heroku.

Largely copied from the [Deno buildpack](https://github.com/chibat/heroku-buildpack-deno) and [Node.js buildpack](https://github.com/heroku/heroku-buildpack-nodejs).

## How to use

To add the buildpack to your Heroku app, visit the settings page for your app on Heroku, then under 'Buildpacks' add the URL `https://github.com/jakeg/heroku-buildpack-bun`.

You'll need a [`Procfile`](https://devcenter.heroku.com/articles/procfile) in the root folder of your app, with eg `web: bun index.js` in it.

Pin a certain Bun version with a `runtime.bun.txt` or `runtime.txt` with e.g. `v1.0.7` in it.

## Support scripts

This buildpack automatically runs the following bun commands and scripts if defined in `package.json`.

- install (`bun install`)
- heroku-prebuild (`bun run heroku-prebuild`)
- build (`bun run build`)
- heroku-postbuild (`bun run heroku-postbuild`)

## Binding to correct port

Bind to `env.PORT` eg

```js
import { env } from 'process'

const server = Bun.serve({
  port: env.PORT || 3000,
  fetch(request) {
    return new Response(`Welcome to Bun running on Heroku!`)
  },
})

console.log(`Listening on localhost:${server.port}`)
```

## Potential issues

~Be aware that Heroku doesn't use a new enough version of the Linux kernel to support `io_uring`, which is needed for `Bun.write()`. Use `node:fs.writeFile()` instead.~ - this [seems now to be fixed](https://devcenter.heroku.com/changelog-items/2713).

Use the Issues tab to report any issues.
