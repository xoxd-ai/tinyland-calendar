# @tummycrypt/tinyland-calendar

Calendar system with CalDAV, iCal, RRULE and timezone support.

## Consume (Bazel only)

This package is distributed as the Bazel module `tummycrypt_tinyland_calendar`
from [xoxd-ai/bazel-registry](https://github.com/xoxd-ai/bazel-registry). It is
not published to npm.

```starlark
bazel_dep(name = "tummycrypt_tinyland_calendar", version = "1.0.0")
```

Link `@tummycrypt_tinyland_calendar//:pkg` into your app's `node_modules` with
`npm_link_package`, then import `@tummycrypt/tinyland-calendar`.

## Develop

```bash
pnpm install
pnpm typecheck
pnpm test
bazel test //:test && bazel build //:pkg
```

Toolchain: TypeScript 7.0.2 and vitest 5.0.3, pinned exactly. See
[CHANGELOG.md](CHANGELOG.md).
