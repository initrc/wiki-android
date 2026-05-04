---
title: "Migrate Value-Based TextField To State-Based TextField"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-text-field-migration
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/text/migrate-state-based"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Migrate Value-Based TextField To State-Based TextField

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/text/migrate-state-based

## Summary

Official examples for replacing value-based `TextField(value, onValueChange)` code with state-based `TextField(state = ...)` code.

## Key Claims

- Basic migration replaces `value`, `onValueChange`, and remembered string state with `rememberTextFieldState()`.
- `singleLine = true` becomes `TextFieldLineLimits.SingleLine`.
- Filtering previously done in `onValueChange` should move to `InputTransformation`.
- Formatting previously done with `VisualTransformation` can move to `OutputTransformation`.
- Keeping `TextFieldState` in a `ViewModel` can be acceptable because it is a snapshot-backed state holder, but save/restore must be handled separately when it is not initialized with `rememberTextFieldState()`.

## Concepts Touched

- [[compose-state]]

## Follow-Up Questions

- Should this wiki add a migration checklist for existing value-based text field code?
