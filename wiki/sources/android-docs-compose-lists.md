---
title: "Lists And Grids"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-lists
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/lists"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Lists And Grids

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/lists

## Summary

Official guide to displaying collections with `Column`, `Row`, lazy lists, lazy grids, keys, list state, paging, and lazy layout performance tips.

## Key Claims

- Use simple `Column` or `Row` for non-scrolling collections when all items can be emitted directly.
- Use lazy layouts for large or unknown-length collections because they compose and lay out visible items.
- `contentPadding` applies to lazy content, not to the lazy container itself.
- Stable unique keys preserve item state across dataset changes; on Android, keys must be `Bundle`-supported for saveable state restoration.
- `rememberLazyListState()` allows code to read and control lazy list scroll position.
- `scrollToItem()` and `animateScrollToItem()` are suspending functions.
- `derivedStateOf` and `snapshotFlow` are useful for specific scroll-position reactions.
- Lazy layout performance guidance includes avoiding zero-pixel items, same-direction nested scroll without fixed size, and too many independent elements in one item.

## Concepts Touched

- [[compose-lists]]
- [[compose-effects]]
- [[compose-state]]
- [[compose-practice-problems]]

## Follow-Up Questions

- Should this wiki add a dedicated page for lazy grid and paging integration?
