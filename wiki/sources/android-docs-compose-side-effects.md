---
title: "Side-Effects In Compose"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-side-effects
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/side-effects"
captured_at: 2026-05-04
tags:
  - android
  - compose
  - lifecycle
---

# Side-Effects In Compose

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/side-effects

## Summary

Official guide to side-effect APIs including `LaunchedEffect`, `rememberCoroutineScope`, `rememberUpdatedState`, `DisposableEffect`, `SideEffect`, `produceState`, `derivedStateOf`, and `snapshotFlow`.

## Key Claims

- Composables should ideally be side-effect free; effect APIs run side effects in predictable composition-aware contexts.
- Effects should be UI-related and should not break unidirectional data flow.
- `LaunchedEffect` launches a coroutine when entering composition, cancels when leaving, and restarts when keys change.
- `rememberCoroutineScope` returns a composition-bound scope for launching coroutines outside composable calls, such as event handlers.
- `rememberUpdatedState` lets long-lived effects use current values without restarting.
- `DisposableEffect` is for effects that need cleanup and must include `onDispose`.
- `derivedStateOf` should be reserved for cases where inputs change more often than the UI should recompose.
- `snapshotFlow` converts Compose state reads into a cold Flow with distinct-until-changed-like emission behavior.

## Concepts Touched

- [[compose-effects]]
- [[compose-state]]
- [[compose-lists]]
- [[compose-practice-problems]]

## Follow-Up Questions

- Should this wiki add examples of bad effect keys and their fixes?
