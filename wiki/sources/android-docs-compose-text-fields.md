---
title: "Configure Text Fields"
kind: source
status: active
last_updated: 2026-05-04
source_id: android-docs-compose-text-fields
source_type: official-doc
authority: primary
url: "https://developer.android.com/develop/ui/compose/text/user-input"
captured_at: 2026-05-04
tags:
  - android
  - compose
---

# Configure Text Fields

## Bibliographic Metadata

- Publisher: Android Developers
- Author: Google
- Published: Unknown
- Updated: Current as captured on 2026-05-04
- Captured: 2026-05-04
- URL: https://developer.android.com/develop/ui/compose/text/user-input

## Summary

Official documentation for Compose text fields, including state-based text fields, value-based text fields, text field state, line limits, transformations, and keyboard options.

## Key Claims

- Official docs recommend state-based text fields because they provide a more complete and reliable text input state model.
- State-based text fields use `TextFieldState`, commonly created with `rememberTextFieldState()`.
- State-based text fields are marked experimental and rely on Material 3 `1.4.0-alpha14` in the captured docs.
- `InputTransformation` filters input before it is committed to state.
- `OutputTransformation` formats displayed output without changing underlying state and removes the need to provide manual offset mapping.
- `SecureTextField` is the state-based Material 3 password-oriented text field.

## Concepts Touched

- [[compose-state]]
- [[compose-practice-problems]]

## Follow-Up Questions

- When state-based text fields leave experimental status, update the version constraint and status notes.
