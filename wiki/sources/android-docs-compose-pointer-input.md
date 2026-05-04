---
title: "Pointer Input, Tap, And Drag In Compose"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-pointer-input
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/touch-input/pointer-input"
captured_at: 2026-05-04
tags:
  - android
  - compose
  - accessibility
---

# Pointer Input, Tap, And Drag In Compose

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/touch-input/pointer-input
- Additional official pages used: https://developer.android.com/develop/ui/compose/touch-input/pointer-input/tap-and-press; https://developer.android.com/develop/ui/compose/touch-input/pointer-input/drag-swipe-fling

## Summary

Official guidance for high-level gestures, lower-level pointer input, click handling, combined clicks, tap detectors, drag detectors, and swipe or drag APIs.

## Key Claims

- Prefer high-level gesture APIs when they fit because they include accessibility, focus, keyboard, hover, and visual indication behavior.
- `clickable` handles clicks broadly, including mouse, finger, keyboard, and accessibility service activation.
- `combinedClickable` supports long click and double click behavior in addition to normal click behavior.
- `pointerInput` with detectors such as `detectTapGestures` or `detectDragGestures` is appropriate when lower-level control is needed.
- `draggable` detects single-axis drag but does not move content by itself; the app owns state and renders movement.
- Material `swipeable` has been replaced by Foundation `anchoredDraggable` APIs starting in Jetpack Compose `1.6.0-alpha01`.

## Concepts Touched

- [[compose-input-and-gestures]]
- [[compose-modifiers]]
- [[compose-practice-problems]]

## Follow-Up Questions

- Should this wiki add a dedicated page for `anchoredDraggable` migration?
