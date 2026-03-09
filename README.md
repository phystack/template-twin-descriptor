# template-twin-descriptor

Starter template for Phystack twin descriptors. Used by `@phystack/cli` to scaffold a new twin descriptor project.

## Overview

A twin descriptor defines the schema for a digital twin on the Phystack platform -- its actions, events, desired properties, and reported properties. This template provides a working example that developers can customize after scaffolding. The TypeScript schema is compiled to JSON Schema at build time and published to the platform via the Phystack CLI.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Language | TypeScript 5 |
| Runtime | Node.js 20+ |
| Schema compiler | `@phygrid/ts-schema` |
| CLI | `@phygrid/cli` (`phy`) |
| Package manager | Yarn 1.x |

## Prerequisites

- Node.js 20+
- Yarn
- Phystack CLI (`phy`) installed globally or via npx

## Getting Started

```bash
# Scaffold a new twin descriptor (via CLI)
phy descriptor create my-descriptor

# Or work directly from the template
cd repos/template-twin-descriptor
yarn install
yarn build
```

## Usage

### Scaffolding with the CLI

```bash
phy descriptor create <name>
```

The CLI copies this template into a new directory, updates `package.json` with the descriptor name, and installs dependencies. From there you edit `src/schema.ts` to define your twin's contract.

### Building

```bash
yarn build
```

This compiles `src/schema.ts` into JSON Schema and writes the output to `build/<version>/`.

### Publishing

```bash
yarn pub
# or equivalently
phy descriptor publish
```

Publishes the compiled schema to the Phystack platform so that the Console can render configuration forms and devices can validate payloads.

## Project Structure

```
src/
  schema.ts       # Twin descriptor schema (actions, events, properties)
build/            # Compiled JSON Schema output (gitignored)
package.json
tsconfig.json
```

## Schema Reference

The `Schema` interface in `src/schema.ts` has four top-level sections:

| Section | Purpose |
|---------|---------|
| `actions` | RPC-style methods the twin exposes (params and return types) |
| `events` | Events the twin can emit (payload types) |
| `desiredProperties` | Configuration set from the Console (renders as a form) |
| `reportedProperties` | Read-only state reported by the device |

TypeScript annotations on `desiredProperties` control Console form rendering:

| Annotation | Effect |
|------------|--------|
| `@title` | Field label in the Console |
| `@default` | Pre-filled default value |
| `@widget color` | Color picker |
| `@widget css` | CSS editor |
| `@widget textarea` | Multi-line text input |
| `@widget javascript` | JavaScript editor |
| `@ui mediaPicker` | Media asset picker |
| `@ui queuePicker` | Queue selector |
| `@ui spacePicker` | Space selector (with optional filter types) |

## Related Documentation

- [Twin descriptor schema guide](https://docs.phystack.com/twin-descriptors) (platform docs)
