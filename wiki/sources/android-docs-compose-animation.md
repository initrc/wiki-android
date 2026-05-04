---
title: "Compose Animation APIs"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-animation
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/animation/choose-api"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Compose Animation APIs

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/animation/choose-api
- Additional official page used: https://developer.android.com/develop/ui/compose/animation/composables-modifiers

## Summary

Official animation API selection guidance and built-in animation composable/modifier documentation.

## Key Claims

- Use the animation decision tree to choose APIs based on whether the work is art-based, repeating, layout-driven, visibility-driven, content-switching, gesture-driven, or value-driven.
- `AnimatedVisibility` animates appearance and disappearance and removes content from composition after exit animations finish.
- `AnimatedContent` animates when target state changes and requires using the lambda `targetState` parameter in emitted content.
- `Crossfade` switches between layouts with a crossfade.
- `animateContentSize` animates size changes and should be placed before size modifiers for smooth layout animation.
- `animate*AsState`, `updateTransition`, `Animatable`, `rememberInfiniteTransition`, and lazy `animateItem()` serve different animation needs.

## Concepts Touched

- [[compose-drawing-and-animation]]
- [[compose-lists]]
- [[compose-practice-problems]]

## Follow-Up Questions

- Should this wiki add a page that maps common UI animation use cases to Compose APIs?
