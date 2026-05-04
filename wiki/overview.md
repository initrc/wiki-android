---
title: "Android Development Wiki Overview"
kind: overview
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
---

# Android Development Wiki Overview

This wiki is a maintained knowledge base for Android development. Its first ingested source is a ChatGPT-generated Jetpack Compose note, so current Compose claims should be treated as useful working notes rather than primary-source facts until official Android documentation is ingested.

## Current Coverage

The wiki currently covers Jetpack Compose fundamentals:

- [[jetpack-compose]] as the library entry point.
- [[compose-layout]] for `Column`, `Row`, `Box`, sizing, spacing, alignment, and weight.
- [[compose-modifiers]] for modifier order, click target sizing, padding, offset, clipping, background, borders, and shapes.
- [[compose-state]] for declarative UI, local state, saveable state, state hoisting, and text fields.
- [[compose-lists]] for `LazyColumn`, stable keys, and remembered list state.
- [[compose-effects]] for composition-tied side effects and coroutine launching.
- [[compose-input-and-gestures]] for clicks, combined clicks, tap detection, pointer input, and drag gestures.
- [[compose-drawing-and-animation]] for drawing modifiers, `Canvas`, and common animation APIs.
- [[compose-practice-problems]] for small exercises that apply the concepts.

## Reliability Notes

- The current Compose synthesis is based on [[chatgpt-jetpack-compose-notes]], a local ChatGPT-generated Markdown note.
- Treat these pages as `needs-review` where they describe API behavior or recommendations that should be validated against official docs.
- Official Android documentation should be ingested next for Compose state, modifiers, lists, effects, and text input.
