---
title: "Jetpack Compose"
kind: library
status: needs-review
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
  - jetpack
  - compose
---

# Jetpack Compose

Jetpack Compose is the current wiki's first major Android UI topic. The local source presents Compose as declarative UI where the screen is described as a function of state: when state changes, composables that read that state can be recomposed.

## Working Mental Model

- Model the screen state first.
- Build composables around that state.
- Keep UI as a function of state.
- Hoist state when multiple composables need it.
- Keep side effects out of the rendering path.

## Topic Map

- [[compose-layout]] covers `Column`, `Row`, `Box`, sizing, spacing, alignment, and weight.
- [[compose-modifiers]] covers modifier ordering and visual/input consequences.
- [[compose-state]] covers `remember`, `rememberSaveable`, state hoisting, and text input.
- [[compose-lists]] covers `LazyColumn`, stable keys, and list scroll state.
- [[compose-effects]] covers composition-tied work and coroutine patterns.
- [[compose-input-and-gestures]] covers click handling and low-level gesture APIs.
- [[compose-drawing-and-animation]] covers custom drawing and animation APIs.
- [[compose-practice-problems]] captures exercises for reinforcing these concepts.

## Reliability

This page is based on [[chatgpt-jetpack-compose-notes]], a ChatGPT-generated local note. It should be verified with official Android documentation before being used as a primary reference.
