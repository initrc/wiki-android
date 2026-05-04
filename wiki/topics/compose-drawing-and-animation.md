---
title: "Compose Drawing And Animation"
kind: topic
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-graphics-modifiers
  - android-docs-compose-animation
  - android-docs-compose-modifiers
tags:
  - android
  - compose
---

# Compose Drawing And Animation

The official docs cover drawing modifiers, `graphicsLayer`, and a decision tree for choosing animation APIs. The local note's simple drawing and animation list aligns with those docs, with a few added caveats below.

## Drawing

Use drawing modifiers when custom visuals are attached to an existing composable:

- `drawBehind` draws before content.
- `drawWithContent` lets code decide whether custom drawing happens before or after content; call `drawContent()` when the composable's normal content should render.
- `drawWithCache` caches drawing objects such as `Brush`, `Shader`, or `Path` while the draw size and read state values remain unchanged.

Use `Canvas` when drawing is the main content.

Only use `drawWithCache` when there is something meaningful to cache. The official docs warn that using it without cached objects can add unnecessary lambda allocation.

## Styling With Drawing-Related Modifiers

The source groups `background`, `clip`, `border`, `alpha`, and `shadow` as common style modifiers. For shaped backgrounds, it notes that `background(color, shape)` may be enough when child content does not need clipping, while `clip` is needed when children must be clipped.

`graphicsLayer` applies draw-layer behavior and transformations such as scale, translation, rotation, alpha, clipping, and compositing strategy. It affects the draw phase, not measurement or placement, so transformed content can visually overlap neighboring layout.

## Animation

Common simple animation APIs in the source:

- `animateFloatAsState`
- `animateDpAsState`
- `AnimatedVisibility`
- `AnimatedContent`
- `updateTransition`

The examples animate alpha, size, visibility, and content changes based on state.

The official decision tree adds:

- Use `AnimatedVisibility` for appearance and disappearance; content is removed from composition after exit animations complete.
- Use `AnimatedContent` or `Crossfade` when switching between different composable content. In `AnimatedContent`, use the lambda's `targetState` parameter in the emitted content so the API can key content correctly.
- Use `animate*AsState` for simple independent value animations with predefined target values.
- Use `updateTransition` when multiple properties are tied to the same state and need coordinated transitions.
- Use `Animatable` for gesture-driven or suspend-controlled animations.
- Place `animateContentSize()` before size modifiers such as `size` or `defaultMinSize` when animating size changes.

## Related Pages

- [[compose-modifiers]]
- [[compose-state]]
- [[compose-input-and-gestures]]
