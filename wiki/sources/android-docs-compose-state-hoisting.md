---
title: "State Hoisting In Jetpack Compose"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-state-hoisting
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/state-hoisting"
captured_at: 2026-05-04
tags:
  - android
  - compose
  - architecture
---

# State Hoisting In Jetpack Compose

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/state-hoisting

## Summary

Official guidance on choosing where UI state belongs based on UI logic, business logic, and lifecycle ownership.

## Key Claims

- UI state should be hoisted to the lowest common ancestor of the composables that read and write it.
- State should remain as close as possible to where it is consumed.
- Plain state holders are useful when UI logic or UI element state becomes complex.
- `ViewModel` is appropriate as a screen-level state holder when business logic or screen UI state is involved.
- `ViewModel` instances should not be passed down to arbitrary reusable child composables; pass state and events instead.
- Some Compose UI element state exposes suspend functions that require a composition-scoped coroutine context for animation-related work.

## Concepts Touched

- [[compose-state]]
- [[compose-lists]]
- [[compose-effects]]

## Follow-Up Questions

- Should this wiki add examples of plain state holder classes for reusable Compose components?
