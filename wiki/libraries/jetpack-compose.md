---
title: "Jetpack Compose"
kind: library
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-documentation
  - android-docs-compose-mental-model
  - android-docs-compose-state
  - android-docs-compose-side-effects
tags:
  - android
  - jetpack
  - compose
---

# Jetpack Compose

Jetpack Compose is Android's modern declarative UI toolkit. The official docs describe Compose as an API for rendering UI without imperatively mutating view objects: app logic provides state, composables transform that state into UI, and UI events request state changes.

## Working Mental Model

- Model screen state first, then pass it into composables.
- Treat composables that emit UI as fast, idempotent, and side-effect free.
- Let events flow up to app logic, and let state flow back down.
- Hoist state when callers, siblings, UI logic, or business logic need to control it.
- Use Compose effect APIs for UI-related side effects that must be tied to composition.

## Recomposition Notes

Recomposition is not a reliable place for side effects. Compose can skip recomposition for unchanged inputs, restart or cancel optimistic recomposition, and run composables often during animations. The durable rule is to make rendering code a pure description of the current UI and move expensive or state-changing work outside composition or into the appropriate effect or state holder.

## Topic Map

- [[compose-layout]] covers `Column`, `Row`, `Box`, sizing, spacing, alignment, and weight.
- [[compose-modifiers]] covers modifier ordering and visual/input consequences.
- [[compose-state]] covers `remember`, `rememberSaveable`, state hoisting, and text input.
- [[compose-lists]] covers `LazyColumn`, stable keys, and list scroll state.
- [[compose-effects]] covers composition-tied work and coroutine patterns.
- [[compose-input-and-gestures]] covers click handling and low-level gesture APIs.
- [[compose-drawing-and-animation]] covers custom drawing and animation APIs.
- [[compose-practice-problems]] captures exercises for reinforcing these concepts.

## Official Review

The local note's high-level mental model aligns with the official Compose documentation. The official docs add stronger constraints: composables should be side-effect free, state changes should drive recomposition through observable state, and effect APIs should be used for predictable side effects.
