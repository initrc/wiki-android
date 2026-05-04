---
title: "Compose Input And Gestures"
kind: topic
status: needs-review
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
  - compose
  - accessibility
---

# Compose Input And Gestures

The source separates normal click handling from lower-level gesture handling.

## Clicks

For normal clicks, the source recommends high-level modifiers such as `clickable`. It notes that these modifiers include useful behavior such as accessibility support and visual feedback.

For combined click behavior, the source lists `combinedClickable` with `onClick` and `onLongClick`.

## Pointer Input

Use `pointerInput` for lower-level gesture detection, such as custom tap detection or drag handling.

Examples touched by the source:

- `detectTapGestures(...)` for tap and long-press callbacks.
- `detectDragGestures(...)` for drag input.
- `change.consume()` while handling drag events.
- `Modifier.offset { IntOffset(...) }` to render dragged position.

## Modifier Order And Click Targets

Click behavior is tightly related to [[compose-modifiers]]. The source's rule is to put `clickable` after modifiers that define the area to be clickable and before modifiers that only add internal spacing.

## Related Pages

- [[compose-modifiers]]
- [[compose-effects]]
- [[compose-state]]
