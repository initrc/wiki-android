---
title: "Compose Modifiers"
kind: topic
status: needs-review
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
  - compose
---

# Compose Modifiers

Modifiers define layout, sizing, interaction, drawing, clipping, background, borders, and other behavior in Compose. The source emphasizes that modifier order is part of the behavior, not cosmetic style.

## Ordering

Modifier order changes results because modifiers are applied in sequence. The source highlights common cases:

- `background` before `padding` creates internal space inside the decorated area.
- `padding` before `background` applies the background to the padded layout.
- `clickable` should come after modifiers that define the area intended to be clickable and before modifiers that are only internal visual spacing.

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

## Padding Versus Offset

- `padding` affects measurement and layout space.
- `offset` moves the composable visually after layout.

The source suggests `padding` for normal spacing and `offset` for badges, animations, and small visual nudges.

## Shape, Background, Border, And Clip

For card-like UI, the source describes this common order:

```text
clip -> background -> border -> padding
```

It also notes that `background(color, shape)` can avoid a separate `clip` when child content does not need to be clipped. Use `clip` when child content must respect the shape.

## Related Pages

- [[compose-layout]]
- [[compose-input-and-gestures]]
- [[compose-drawing-and-animation]]
