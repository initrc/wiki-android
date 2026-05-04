---
title: "Compose Effects"
kind: topic
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-side-effects
  - android-docs-compose-mental-model
  - android-docs-compose-state
tags:
  - android
  - compose
  - lifecycle
---

# Compose Effects

Effects handle UI-related work that happens because of composition but is not itself UI rendering. The official docs define an effect as a composable that does not emit UI and causes side effects to run after composition reaches a controlled lifecycle point.

Do not use effects as a general escape hatch. Effects should stay UI-related and should not break unidirectional data flow.

## LaunchedEffect

`LaunchedEffect` is used for suspend work tied to composition.

- `LaunchedEffect(Unit)` runs once for a composable instance.
- `LaunchedEffect(query)` cancels and restarts when `query` changes.

When `LaunchedEffect` enters the Composition it launches a coroutine. The coroutine is canceled when the effect leaves the Composition, and restarted when any key changes. A constant key such as `Unit` or `true` makes the effect follow the lifecycle of the call site; the official docs warn to pause before using that pattern.

## rememberCoroutineScope

`rememberCoroutineScope()` is used when a coroutine starts from an event handler, such as a button click.

Working distinction from the source:

```text
LaunchedEffect(...)      -> start because composable appeared or key changed
rememberCoroutineScope() -> start because user clicked/swiped/etc.
```

The returned scope is bound to the point in the Composition where it is called and is canceled when that call leaves the Composition.

## DisposableEffect

`DisposableEffect` is used when a side effect needs cleanup through `onDispose`, such as registering and unregistering a lifecycle observer.

`DisposableEffect` must end with an `onDispose` clause. An empty `onDispose` is usually a signal that another effect API may fit better.

## rememberUpdatedState

`rememberUpdatedState` lets an effect use the latest callback or value without restarting the effect.

## derivedStateOf

`derivedStateOf` is used when inputs change more often than the UI needs to recompose, such as scroll position crossing a threshold. It is expensive enough that it should not be used for trivial derived values that must update exactly as often as their inputs, such as concatenating first and last name.

## snapshotFlow

`snapshotFlow` converts Compose state reads into a cold Flow. It emits when a read `State` object changes and the new result is not equal to the previous emitted result, similar to `distinctUntilChanged`.

## Other Effect APIs

- `SideEffect` publishes Compose state to non-Compose code after every successful recomposition.
- `produceState` converts external or callback-based state into Compose `State`; internally it combines `remember { mutableStateOf(...) }` with `LaunchedEffect`.

## Restart Keys

Mutable and immutable values used inside an effect block should generally be passed as keys so the effect restarts when those values change. If a value should stay current without restarting the effect, wrap it in `rememberUpdatedState`.

## Related Pages

- [[compose-state]]
- [[compose-lists]]
- [[compose-input-and-gestures]]
