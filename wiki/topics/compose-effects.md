---
title: "Compose Effects"
kind: topic
status: needs-review
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
  - compose
  - lifecycle
---

# Compose Effects

Effects handle work that happens because of composition but is not itself UI rendering. The source emphasizes keeping side effects out of the rendering path.

## LaunchedEffect

`LaunchedEffect` is used for suspend work tied to composition.

- `LaunchedEffect(Unit)` runs once for a composable instance.
- `LaunchedEffect(query)` cancels and restarts when `query` changes.

## rememberCoroutineScope

`rememberCoroutineScope()` is used when a coroutine starts from an event handler, such as a button click.

Working distinction from the source:

```text
LaunchedEffect(...)      -> start because composable appeared or key changed
rememberCoroutineScope() -> start because user clicked/swiped/etc.
```

## DisposableEffect

`DisposableEffect` is used when a side effect needs cleanup through `onDispose`, such as registering and unregistering a lifecycle observer.

## rememberUpdatedState

`rememberUpdatedState` lets an effect use the latest callback or value without restarting the effect.

## derivedStateOf

`derivedStateOf` is used for derived values that should update only when inputs meaningfully change. The source calls out scroll-derived UI as a common use case.

## snapshotFlow

`snapshotFlow` converts Compose state reads into a Flow. The source demonstrates it inside `LaunchedEffect` to observe a lazy list's first visible item index.

## Related Pages

- [[compose-state]]
- [[compose-lists]]
- [[compose-input-and-gestures]]
