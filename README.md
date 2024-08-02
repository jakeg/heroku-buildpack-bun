# heroku-buildpack-bun

Heroku buildpack for [Bun.js](https://bun.sh/) - allows you to run Bun on Heroku.

Largely copied from the [Deno buildpack](https://github.com/chibat/heroku-buildpack-deno) and [Node.js buildpack](https://github.com/heroku/heroku-buildpack-nodejs).

## How to use

To add the buildpack to your Heroku app, visit the settings page for your app on Heroku, then under 'Buildpacks' add the URL `https://github.com/jakeg/heroku-buildpack-bun`.

You'll either need a [`Procfile`](https://devcenter.heroku.com/articles/procfile) in the root folder of your app (with eg `web: bun index.js` in it), or a `package.json` with a start script listed.

Pin a certain Bun version such as `v1.1.20` with the `BUN_VERSION` environment variable (eg under 'Config Vars' on your app's Heroku settings page), or with a `.bun-version`, `runtime.bun.txt` or `runtime.txt` containing a single line for the pinned version. The version can be specified with or without a leading `v` eg `v1.0.7` or `1.0.7` or [any other Bun tags](https://github.com/oven-sh/bun/tags).

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

Use the Issues tab to report any issues.
