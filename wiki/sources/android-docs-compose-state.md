---
title: "State In Jetpack Compose"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-state
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/state"
captured_at: 2026-05-04
tags:
  - android
  - compose
  - architecture
---

# State In Jetpack Compose

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/state

## Summary

Official guide to state, composition, `remember`, `mutableStateOf`, `rememberSaveable`, observable state adapters, state hoisting, and state holders.

## Key Claims

- Compose UI updates by calling composables with new arguments or by recomposing composables that read changed observable state.
- `remember` stores values in the Composition and forgets them when the calling composable leaves the Composition.
- `rememberSaveable` can retain state across recomposition and activity or process recreation through saved instance state, subject to saveability limits.
- Non-observable mutable objects such as mutable lists can cause stale UI because Compose is not notified when they change.
- Flow should be collected as Compose state, with `collectAsStateWithLifecycle()` recommended for Android apps.
- State hoisting replaces internal state with value and event parameters and supports unidirectional data flow.

## Concepts Touched

- [[compose-state]]
- [[compose-effects]]
- [[compose-lists]]
- [[jetpack-compose]]

## Follow-Up Questions

- Should the wiki split observable state adapters and state saving into separate pages?
