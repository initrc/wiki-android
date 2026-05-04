---
title: "Compose Modifiers"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-modifiers
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/modifiers"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Compose Modifiers

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/modifiers

## Summary

Official guide to modifier usage, ordering, built-in layout modifiers, scope safety, and modifier reuse.

## Key Claims

- Modifiers can change size, layout, behavior, appearance, accessibility information, input handling, and high-level interactions.
- All reusable composables should accept a `modifier` parameter and pass it to the first child that emits UI.
- Modifier order is significant.
- `clickable().padding(...)` makes the padding clickable; `padding(...).clickable()` leaves the padding outside the click target.
- `offset` changes visual position without changing measurements.
- Scoped modifiers such as `matchParentSize` and `weight` only work for direct children in their matching scopes.
- Extracting and reusing modifier chains can improve readability and reduce repeated allocation in recomposition.

## Concepts Touched

- [[compose-modifiers]]
- [[compose-input-and-gestures]]
- [[compose-layout]]
- [[glossary]]

## Follow-Up Questions

- Should the wiki add examples of recommended `modifier` parameter placement for custom composables?
