---
title: "Compose Practice Problems"
kind: pattern
status: draft
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-state
  - android-docs-compose-lists
  - android-docs-compose-side-effects
  - android-docs-compose-pointer-input
  - android-docs-compose-animation
tags:
  - android
  - compose
  - testing
---

# Compose Practice Problems

These exercises come from [[chatgpt-jetpack-compose-notes]] and remain useful after official-doc review. Use the linked topic pages for current API details when writing solutions.

## Todo List

Build a todo list with:

- `TextField`
- Add button
- `LazyColumn` of todos
- Click-to-toggle rows
- Delete button per row
- Empty state

Skills: [[compose-state]], [[compose-lists]], [[compose-layout]], and [[compose-input-and-gestures]].

## Search And Filter List

Build a searchable list of hardcoded contacts:

- Search `TextField`
- Filter as the user types
- Show a no-results state

Skills: derived UI state, text input, and [[compose-lists]]. Use `derivedStateOf` only if filtering inputs change more often than the UI should recompose; a plain derived local value is enough when the filtered list should update exactly when the query or source list changes.

## Timer

Build a timer with:

- Start, pause, and reset
- Text showing elapsed seconds
- A `LaunchedEffect` loop

Skills: [[compose-effects]], coroutine cancellation, and [[compose-state]]. Key `LaunchedEffect` to the timer's running state or controlling inputs so the loop starts and cancels predictably.

## Drag Card

Build a horizontally draggable card that animates back to center on release.

Skills: [[compose-input-and-gestures]], `offset`, and [[compose-drawing-and-animation]]. A high-level `draggable` can detect single-axis drag, but the solution still owns offset state and renders movement.

## Follow-Up

These exercises should eventually gain solution pages or links to runnable sample projects.
