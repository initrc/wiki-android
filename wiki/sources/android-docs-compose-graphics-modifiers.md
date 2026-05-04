---
title: "Drawing And Graphics Modifiers In Compose"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-graphics-modifiers
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/graphics/draw/modifiers"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Drawing And Graphics Modifiers In Compose

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/graphics/draw/modifiers

## Summary

Official guide to Compose drawing modifiers, `graphicsLayer`, transformations, clipping, alpha, and compositing strategies.

## Key Claims

- Compose drawing commands are done with drawing modifiers such as `drawWithContent`, `drawBehind`, and `drawWithCache`.
- `Canvas` is a convenient wrapper around `Modifier.drawBehind`.
- `drawWithContent` requires calling `drawContent()` when normal content should render.
- `drawWithCache` caches drawing objects while draw size and read state values remain unchanged and should only be used when caching is needed.
- `graphicsLayer` applies drawing isolation, transformations, rasterization, clipping, alpha, and compositing behavior.
- `graphicsLayer` does not change measured size or placement.

## Concepts Touched

- [[compose-drawing-and-animation]]
- [[compose-modifiers]]

## Follow-Up Questions

- Should this wiki split drawing modifiers and `graphicsLayer` into separate pages?
