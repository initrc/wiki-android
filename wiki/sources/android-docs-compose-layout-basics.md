---
title: "Compose Layout Basics"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-layout-basics
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/layouts/basics"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Compose Layout Basics

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/layouts/basics

## Summary

Official guide to Compose layout primitives, the layout model, performance, responsive constraints, and slot-based layouts.

## Key Claims

- Compose transforms state into UI through composition, layout, and drawing.
- `Column`, `Row`, and `Box` are standard layout components for vertical stacking, horizontal stacking, and overlaying content.
- `Row` and `Column` provide arrangement and alignment parameters.
- Compose lays out the UI tree in a single pass and normally measures children only once.
- Nested Compose layouts are efficient compared with problematic nested View hierarchies.
- Modifiers are essential for customizing layout.
- `BoxWithConstraints` exposes parent constraints to the composable.

## Concepts Touched

- [[compose-layout]]
- [[compose-modifiers]]
- [[jetpack-compose]]

## Follow-Up Questions

- Should this wiki add a page for `Scaffold` and slot APIs?
