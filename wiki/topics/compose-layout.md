---
title: "Compose Layout"
kind: topic
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-layout-basics
  - android-docs-compose-modifiers
  - android-docs-compose-modifier-constraints
tags:
  - android
  - compose
  - views
---

# Compose Layout

Compose layout in the official docs is part of the pipeline where state becomes UI through composition, layout, and drawing. The practical starting point is still three standard primitives: `Column`, `Row`, and `Box`.

## Core Primitives

- `Column` stacks children vertically. Its main axis is vertical, so it uses `verticalArrangement`; its cross axis is horizontal, so it uses `horizontalAlignment`.
- `Row` stacks children horizontally. Its main axis is horizontal, so it uses `horizontalArrangement`; its cross axis is vertical, so it uses `verticalAlignment`.
- `Box` overlays or positions children relative to its bounds. Child-level `Modifier.align(...)` is the primary alignment tool.

Compose supports deeply nested layouts efficiently because its layout model avoids repeated child measurement in normal layouts. The UI tree is laid out in a single pass: parents pass constraints down, children report sizes up, and placement follows.

## Sizing

Common sizing modifiers in the source include:

- `fillMaxSize()`
- `fillMaxWidth()`
- `fillMaxHeight()`
- `size(...)`
- `width(...)`
- `height(...)`
- `wrapContentSize()`
- `defaultMinSize(...)`

The official docs distinguish `size` from `requiredSize`: `size` sets a preferred size while still adhering to incoming constraints, while `requiredSize` replaces incoming constraints with exact bounds. When a child overrides constraints, the parent is still told a coerced size and the child is centered unless another modifier changes that placement.

## Weight

`weight` divides remaining space in a `Row` or `Column`.

Common patterns:

- In a form row, give a fixed label width and apply `Modifier.weight(1f)` to the field.
- In a chat-style layout, give the message list `Modifier.weight(1f)` so it occupies remaining vertical space while the input stays at the bottom.
- Use `Spacer(Modifier.weight(1f))` when flexible empty space is needed between items.

`weight` is scope-specific: it is available for direct children of `Row` or `Column` through `RowScope` and `ColumnScope`.

## Spacing And Alignment

The source recommends `Arrangement.spacedBy(...)` when siblings need consistent gaps. It reserves explicit `Spacer` usage for flexible or semantic empty space.

Alignment can be applied at the parent level or child level:

- Parent-level alignment applies to all children in that container.
- Child-level `Modifier.align(...)` affects one child.
- `Box` commonly uses child alignment for corners, center placement, and overlays.

Use `BoxWithConstraints` when a composable needs to choose layout based on the constraints supplied by its parent.

## Related Pages

- [[compose-modifiers]]
- [[compose-state]]
- [[jetpack-compose]]
