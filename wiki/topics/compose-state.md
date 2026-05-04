---
title: "Compose State"
kind: topic
status: needs-review
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
tags:
  - android
  - compose
  - architecture
---

# Compose State

The source presents Compose UI as a function of state. The durable rule is: model screen state first, then describe UI from that state.

## Local State

`remember` stores local UI state across recomposition:

```kotlin
var expanded by remember { mutableStateOf(false) }
```

The source describes this as appropriate when only one composable cares about the state.

## Saveable State

`rememberSaveable` is used for simple UI state that should survive configuration changes:

```kotlin
var text by rememberSaveable { mutableStateOf("") }
```

The source lists text input, selected tabs, and expanded/collapsed state as examples.

## State Hoisting

State hoisting moves state ownership up to a caller. The local source describes the common shape as replacing internal state with a value and event callback:

```kotlin
@Composable
fun NameInput(
    name: String,
    onNameChange: (String) -> Unit
) {
    TextField(
        value = name,
        onValueChange = onNameChange
    )
}
```

Working rule from the source:

- If only one composable cares, keep state local.
- If siblings need it, hoist to their lowest common parent.
- If business logic needs it, use a `ViewModel` or state holder.

## Text Input

The source covers classic value-based `TextField(value, onValueChange)` usage with `rememberSaveable`, labels, `singleLine`, and password visual transformation. It also notes that newer Material 3 APIs include state-based text fields, which should be checked against official documentation before this wiki gives a recommendation.

## Related Pages

- [[jetpack-compose]]
- [[compose-effects]]
- [[compose-lists]]
