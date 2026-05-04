---
title: "Android Wiki Glossary"
kind: glossary
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-mental-model
  - android-docs-compose-state
  - android-docs-compose-modifiers
  - android-docs-compose-lists
  - android-docs-compose-side-effects
tags:
  - android
---

# Android Wiki Glossary

## Compose

Jetpack Compose is represented in this wiki as Android's declarative UI toolkit. See [[jetpack-compose]].

## Composable

A function annotated with `@Composable` that describes UI as a function of state. Current notes emphasize that composables should not perform side effects directly in the rendering path. See [[compose-state]] and [[compose-effects]].

## Recomposition

The process where Compose re-runs composables that read changed state so the UI reflects the new state. See [[compose-state]].

## Composition

The description of UI built by Compose when it executes composables. Initial composition is the first creation of that description; recomposition updates it when data changes. See [[compose-state]].

## State Hoisting

Moving state ownership out of a child composable and into a caller, usually by replacing internal state with a value parameter and event callback. See [[compose-state]].

## Modifier

A chainable object used to decorate or adjust Compose UI, including layout, size, padding, click handling, drawing, background, border, clipping, and gestures. See [[compose-modifiers]].

## LazyColumn

A Compose list container for vertically scrolling lists whose items may grow beyond the screen. See [[compose-lists]].

## Effect

A composable that does not emit UI and runs a side effect at a composition-aware lifecycle point. See [[compose-effects]].
