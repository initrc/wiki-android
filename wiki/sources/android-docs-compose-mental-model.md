---
title: "Jetpack Compose Mental Model"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-mental-model
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/mental-model"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Jetpack Compose Mental Model

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/mental-model

## Summary

Official explanation of Compose as a declarative UI framework and of how recomposition shapes composable design.

## Key Claims

- Compose renders UI declaratively instead of mutating view objects directly.
- Composable functions should be fast, idempotent, and side-effect free.
- UI events notify app logic, app logic changes state, and Compose calls composables again with new data when needed.
- Recomposition can skip unchanged functions, be canceled and restarted, run often during animations, and should not be used for side effects.

## Concepts Touched

- [[jetpack-compose]]
- [[compose-state]]
- [[compose-effects]]
- [[glossary]]

## Follow-Up Questions

- Should this wiki add a dedicated page for recomposition and Compose lifecycle?
