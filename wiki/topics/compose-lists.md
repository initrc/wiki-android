---
title: "Compose Lists"
kind: topic
status: needs-review
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
  - compose
---

# Compose Lists

The source focuses on `LazyColumn` for scrollable vertical lists.

## LazyColumn

The local note presents `LazyColumn` as the default list primitive when the list can grow beyond the visible screen.

Common configuration includes:

- `modifier = Modifier.fillMaxSize()`
- `contentPadding = PaddingValues(...)`
- `verticalArrangement = Arrangement.spacedBy(...)`
- `items(items) { item -> ... }`

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

## List State

`rememberLazyListState()` stores list scroll state and allows programmatic scroll operations, such as `animateScrollToItem(...)` from a coroutine.

## Related Pages

- [[compose-layout]]
- [[compose-state]]
- [[compose-effects]]
