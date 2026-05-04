---
title: "Compose Input And Gestures"
kind: topic
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-pointer-input
  - android-docs-compose-modifiers
tags:
  - android
  - compose
  - accessibility
---

# Compose Input And Gestures

The official docs separate high-level interaction APIs from lower-level pointer input. Prefer the highest abstraction that fits the interaction because high-level APIs include behavior that is easy to miss by hand.

## Clicks

For normal clicks, use high-level APIs such as `clickable` or component-level click handling like `Surface(onClick = ...)`. `clickable` adds more than tap detection: it contributes semantics for accessibility, focus and keyboard support, hover handling, and a visual indication such as ripple.

For combined click behavior, use `combinedClickable` with `onClick`, `onLongClick`, or double-click handlers. The official docs recommend haptic feedback for long-press behavior.

## Pointer Input

Use `pointerInput` for lower-level gesture detection when high-level APIs do not expose the needed behavior or when their extra behavior is not wanted. Examples include a scrim that should dismiss on tap without ripple/focus behavior, or a double-tap image zoom that needs the tap position.

Examples touched by the source:

- `detectTapGestures(...)` for tap and long-press callbacks.
- `detectDragGestures(...)` for drag input.
- `change.consume()` while handling drag events.
- `Modifier.offset { IntOffset(...) }` to render dragged position.

## Drag And Swipe

`draggable` is the high-level entry point for single-axis drag gestures, but it only detects the gesture. The app still owns state and renders movement, commonly through `offset`.

Use `pointerInput` plus `detectDragGestures` when the whole drag gesture needs custom control. The official docs call out `change.consume()` while handling low-level drag events.

The older Material `swipeable` APIs have been replaced by Foundation `anchoredDraggable` APIs starting in Jetpack Compose `1.6.0-alpha01`.

## Modifier Order And Click Targets

Click behavior is tightly related to [[compose-modifiers]]. Official docs show that `clickable().padding(...)` makes the padding clickable, while `padding(...).clickable()` excludes the outer padding from the click target.

## Related Pages

- [[compose-modifiers]]
- [[compose-effects]]
- [[compose-state]]
