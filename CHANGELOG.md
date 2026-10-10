# Changelog

## Unreleased

### Changed

- Dev toolchain: `vite` 8.3.3 is now an exact devDependency (RU1/RU5), so
  vitest 5.0.3 runs on the estate Vite instead of the transitively resolved
  8.0.10. No runtime or package change; no release needed.

## 1.0.0 (2026-10-09)

Major release under the 2026-10-08 estate uplift (RU1, RU6, RU8, RU10, RU13).
The runtime API is unchanged from 0.2.3; the toolchain and the distribution
channel change.

### Changed (breaking for build and distribution, not for the runtime API)

- Toolchain: TypeScript 7.0.2 (native compiler) and vitest 5.0.3, pinned
  exactly. Bazel builds use `aspect_rules_ts` 3.10.1 with the `typescript`
  extension at 7.0.2 (`transpiler = "tsc"`).
- `tsconfig.json` lists `"types": ["node"]` explicitly, because TypeScript 6+
  no longer loads every `@types/*` package by default. `@types/node` moves to
  `^22.0.0` to match `engines.node >= 22`.
- Distribution is Bazel only (RU6): consume the module with
  `bazel_dep(name = "tummycrypt_tinyland_calendar", version = "1.0.0")` from
  xoxd-ai/bazel-registry and link `@tummycrypt_tinyland_calendar//:pkg` with
  `npm_link_package`. The package is marked `private`; the publish workflow,
  `publishConfig` and `prepublishOnly` are removed (RU8). Nothing on npmjs or
  GitHub Packages is unpublished; those versions are deprecated in favour of
  the Bazel module.
- Repository metadata points at xoxd-ai/tinyland-calendar.

### Migration

1. Re-pin: `bazel_dep(name = "tummycrypt_tinyland_calendar", version = "1.0.0")`
   and pin the xoxd-ai/bazel-registry commit that carries it. The module's
   `compatibility_level` stays 1, so 0.2.x and 1.0.0 resolve together under
   minimal version selection.
2. Replace any `@tummycrypt/tinyland-calendar` npm or GitHub Packages
   dependency with the Bazel module linked through `npm_link_package`.
3. Exports, types and behaviour are the same as 0.2.3; no source change is
   needed in consumers. Declarations are now emitted by TypeScript 7, so a
   consumer type-checking against them should use TypeScript 7.0.2 as well.

## 0.2.3

- Standalone repo release (Bazel registry module `tummycrypt_tinyland_calendar`
  0.2.3). No source change from 0.2.2.

## 0.2.2

- Roll forward published package versions so the next release re-establishes
  npm artifact truth for the current repo contents.

## 0.2.1

- Strip `.js.map` sourcemaps from published packages and resolve
  `workspace:*` dependencies to real version ranges.
