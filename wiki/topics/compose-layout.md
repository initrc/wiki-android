---
title: "Compose Layout"
kind: topic
status: needs-review
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
  - compose
  - views
---

# Compose Layout

Compose layout in the source centers on three primitives: `Column`, `Row`, and `Box`.

## Core Primitives

- `Column` stacks children vertically. Its main axis is vertical, so it uses `verticalArrangement`; its cross axis is horizontal, so it uses `horizontalAlignment`.
- `Row` stacks children horizontally. Its main axis is horizontal, so it uses `horizontalArrangement`; its cross axis is vertical, so it uses `verticalAlignment`.
- `Box` overlays or positions children relative to its bounds. Child-level `Modifier.align(...)` is the primary alignment tool.

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

The source distinguishes `size` from `requiredSize`: `size` requests a size while respecting parent constraints; `requiredSize` forces the size more aggressively and should be used rarely.

## Weight

`weight` divides remaining space in a `Row` or `Column`.

Common patterns:

- In a form row, give a fixed label width and apply `Modifier.weight(1f)` to the field.
- In a chat-style layout, give the message list `Modifier.weight(1f)` so it occupies remaining vertical space while the input stays at the bottom.
- Use `Spacer(Modifier.weight(1f))` when flexible empty space is needed between items.

## Spacing And Alignment

The source recommends `Arrangement.spacedBy(...)` when siblings need consistent gaps. It reserves explicit `Spacer` usage for flexible or semantic empty space.

Alignment can be applied at the parent level or child level:

- Parent-level alignment applies to all children in that container.
- Child-level `Modifier.align(...)` affects one child.
- `Box` commonly uses child alignment for corners, center placement, and overlays.

## Related Pages

- [[compose-modifiers]]
- [[compose-state]]
- [[jetpack-compose]]
