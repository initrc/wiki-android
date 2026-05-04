---
title: "Compose State"
kind: topic
status: active
last_updated: 2026-05-04
sources:
  - chatgpt-jetpack-compose-notes
  - android-docs-compose-state
  - android-docs-compose-state-hoisting
  - android-docs-compose-text-fields
  - android-docs-compose-text-field-migration
tags:
  - android
  - compose
  - architecture
---

# Compose State

Compose UI is driven by state. The official docs define state broadly as any value that can change over time, and in Compose the UI updates when composables are called again with new arguments or when observable Compose `State` read by a composable changes.

## Local State

`remember` stores an object in the Composition across recompositions:

```kotlin
var expanded by remember { mutableStateOf(false) }
```

`remember` forgets the object when the calling composable leaves the Composition. It is appropriate for local UI element state when no caller or sibling needs to control it.

## Saveable State

`rememberSaveable` behaves like `remember`, but also saves values through the saved instance state mechanism when possible:

```kotlin
var text by rememberSaveable { mutableStateOf("") }
```

Use it for UI element state that should survive configuration changes and system-initiated process recreation. It automatically saves values supported by `Bundle`; use `@Parcelize`, `mapSaver`, or `listSaver` for custom types. It does not preserve state if the user fully dismisses the activity.

## Observable State

`mutableStateOf` creates observable `MutableState<T>` integrated with the Compose runtime. When its `value` changes, Compose schedules recomposition for composables that read it.

Compose can also consume other observable types after converting them to `State<T>`. On Android, prefer `collectAsStateWithLifecycle()` for `Flow`; use `collectAsState()` for platform-agnostic Compose code. `LiveData`, RxJava2, and RxJava3 have Compose adapters when the matching runtime artifacts are present.

Avoid non-observable mutable containers such as `ArrayList` or `mutableListOf()` as state. They can change without triggering recomposition; prefer immutable lists held by observable state.

## State Hoisting

State hoisting moves state ownership up to a caller. The common shape is replacing internal state with a value and event callback:

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

Official hoisting rules add two more constraints:

- Hoist state to at least the highest level where it may be changed.
- Hoist states together when they change in response to the same events.

Keep UI element state as close as possible to where it is consumed. Use a plain state holder when UI logic becomes complex, and use a screen-level state holder such as a `ViewModel` when business logic or screen UI state is involved. Avoid passing `ViewModel` instances down through reusable child composables; pass state and event lambdas.

## Text Input

The official text field docs now recommend state-based Material 3 text fields for a more complete and reliable text input state model. State-based text fields use `TextFieldState` and `rememberTextFieldState()` instead of the classic `value` plus `onValueChange` loop.

Important version constraint: the official docs mark state-based Material 3 text fields as experimental and tied to Material 3 `1.4.0-alpha14`.

State-based text fields replace:

- `singleLine`, `minLines`, and `maxLines` with `TextFieldLineLimits`.
- `VisualTransformation` use cases with `InputTransformation` for filtering committed input and `OutputTransformation` for formatting displayed output.
- password `TextField` patterns with `SecureTextField` where appropriate.

Value-based `TextField(value, onValueChange)` remains relevant in existing code and for APIs that have not migrated, but new wiki recommendations should call out the state-based path and its experimental status.

## Related Pages

- [[jetpack-compose]]
- [[compose-effects]]
- [[compose-lists]]
