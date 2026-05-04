---
title: "Compose Modifiers"
kind: topic
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-modifiers
  - android-docs-compose-modifier-constraints
  - android-docs-compose-graphics-modifiers
tags:
  - android
  - compose
---

# Compose Modifiers

Modifiers define layout, sizing, behavior, drawing, accessibility metadata, and input handling in Compose. The official docs emphasize that modifier order is part of behavior: each modifier element wraps the rest of the chain and the layout node it is applied to.

## Ordering

Modifier order changes results because modifiers are applied in sequence. Common cases:

- `background` before `padding` creates internal space inside the decorated area.
- `padding` before `background` applies the background to the padded layout.
- `clickable().padding(...)` makes the padding part of the clickable area.
- `padding(...).clickable()` leaves the outer padding outside the click target.

For a full-width clickable row, the source's pattern is:

```kotlin
Row(
    modifier = Modifier
        .fillMaxWidth()
        .clickable { onClick() }
        .padding(16.dp)
) {
    Text("Settings")
}
```

## Constraints And Size

Modifiers that affect measurement modify the constraints passed down the chain. `size` requests preferred bounds while respecting incoming constraints; `requiredSize` overrides incoming constraints with exact bounds. Chaining multiple `size` modifiers does not make the later one override the first, because the first can already make the constraints exact.

`wrapContentSize` can reset minimum constraints and place smaller content inside the available space.

## Padding Versus Offset

- `padding` affects measurement and layout space.
- `offset` moves the composable visually without changing its measurements.

The source suggests `padding` for normal spacing and `offset` for badges, animations, and small visual nudges.

## Shape, Background, Border, And Clip

For card-like UI, the source describes this common order:

```text
clip -> background -> border -> padding
```

It also notes that `background(color, shape)` can avoid a separate `clip` when child content does not need to be clipped. Use `clip` when child content must respect the shape.

## Scope And Reuse

Some modifiers are scope-specific. `matchParentSize` applies only to direct children in `BoxScope`; `weight` applies only to direct children in `RowScope` or `ColumnScope`. Reuse extracted modifier chains when they are stable and shared, especially in frequently recomposing or lazy-layout code. Preserve scope safety when reusing scoped modifiers.

## Correction History

The original raw ChatGPT note reversed one click-target example. It was corrected on 2026-05-04 to match official Android docs: padding added after `clickable` is clickable, while padding added before `clickable` is outside the click target.

## Related Pages

- [[compose-layout]]
- [[compose-input-and-gestures]]
- [[compose-drawing-and-animation]]
