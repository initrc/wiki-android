---
title: "Compose Drawing And Animation"
kind: topic
status: needs-review
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
  - compose
---

# Compose Drawing And Animation

The source covers simple custom drawing and common state-driven animation APIs.

## Drawing

Use drawing modifiers when custom visuals are attached to an existing composable:

- `drawBehind` draws before content.
- `drawWithContent` can call `drawContent()` and then draw after content.
- `drawWithCache` appears in the source's API memory map but is not explained in detail.

Use `Canvas` when drawing is the main content.

## Styling With Drawing-Related Modifiers

The source groups `background`, `clip`, `border`, `alpha`, and `shadow` as common style modifiers. For shaped backgrounds, it notes that `background(color, shape)` may be enough when child content does not need clipping, while `clip` is needed when children must be clipped.

## Animation

Common simple animation APIs in the source:

- `animateFloatAsState`
- `animateDpAsState`
- `AnimatedVisibility`
- `AnimatedContent`
- `updateTransition`

The examples animate alpha, size, visibility, and content changes based on state.

## Related Pages

- [[compose-modifiers]]
- [[compose-state]]
- [[compose-input-and-gestures]]
