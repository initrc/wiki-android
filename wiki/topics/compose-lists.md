---
title: "Compose Lists"
kind: topic
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-lists
  - android-docs-compose-side-effects
tags:
  - android
  - compose
---

# Compose Lists

The official docs cover normal `Column` and `Row` for small non-scrolling collections, and lazy layouts for large or unknown-length collections.

## LazyColumn

Use `LazyColumn` for vertically scrolling lists that can grow beyond the visible screen. Lazy layouts compose and lay out only the items visible in the viewport, unlike a normal `Column` that emits every item.

Common configuration includes:

- `modifier = Modifier.fillMaxSize()`
- `contentPadding = PaddingValues(...)`
- `verticalArrangement = Arrangement.spacedBy(...)`
- `items(items) { item -> ... }`

`contentPadding` applies to the lazy layout's content, not to the `LazyColumn` container itself. `Arrangement.spacedBy(...)` adds space between items.

## Stable Keys

The source recommends stable keys when list items can be inserted, removed, or reordered:

```kotlin
LazyColumn {
    items(
        items = messages,
        key = { it.id }
    ) { message ->
        MessageRow(message)
    }
}
```

By default, lazy item state is keyed by item position. Stable and unique keys let Compose preserve remembered item state across inserts, removals, and reorders. On Android, item keys must be supported by `Bundle` so `rememberSaveable` item state can be restored after activity recreation or after an item leaves and re-enters composition.

## List State

`rememberLazyListState()` stores list scroll state and allows code to read scroll position or control it. `scrollToItem(...)` and `animateScrollToItem(...)` are suspending functions and must be called from a coroutine, commonly one launched from `rememberCoroutineScope()` for event handlers.

For scroll-derived UI, read `LazyListState` in composition when the UI must update, use `derivedStateOf` when the scroll value changes more often than the UI threshold, and use `snapshotFlow` inside `LaunchedEffect` for work such as analytics that does not need to update UI directly.

## Performance Notes

- Avoid zero-pixel lazy items while async content loads; provide realistic placeholder sizes.
- Avoid nesting same-direction scroll containers without a fixed child size. Put headers, lists, and footers into one parent `LazyColumn` where possible.
- Avoid placing many independent elements into one lazy `item` block, because they can no longer be composed individually and scroll indexing becomes less useful.
- Consider `contentType` for lazy lists with multiple item shapes so Compose can reuse item compositions more efficiently.

## Related Pages

- [[compose-layout]]
- [[compose-state]]
- [[compose-effects]]
