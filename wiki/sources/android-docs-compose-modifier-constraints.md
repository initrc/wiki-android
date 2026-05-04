---
title: "Constraints And Modifiers In Compose"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-modifier-constraints
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/layouts/constraints-modifiers"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Constraints And Modifiers In Compose

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/layouts/constraints-modifiers

## Summary

Official explanation of how modifier chains wrap layout nodes and affect constraints, measurement, and placement.

## Key Claims

- Modifier chains wrap layout nodes, and each modifier can affect the constraints passed to the next node.
- Constraints define minimum and maximum width and height bounds.
- `size` adapts incoming constraints as closely as possible to the requested preferred size.
- Chaining multiple `size` modifiers does not make later `size` calls override earlier exact constraints.
- `requiredSize` overrides incoming constraints by passing exact bounds.
- `wrapContentSize` can reset minimum constraints and place child content inside available space.
- Modifier order can change clipping, padding, size, and drawing results.

## Concepts Touched

- [[compose-modifiers]]
- [[compose-layout]]
- [[compose-drawing-and-animation]]

## Follow-Up Questions

- Should this wiki add diagrams or runnable examples for common modifier-order mistakes?
