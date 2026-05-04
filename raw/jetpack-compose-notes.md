# Jetpack Compose notes

Author: ChatGPT 5.5

## 1. Mental model

Compose is **declarative**:

```kotlin
UI = f(state)
```

You do not “update a view.” You update state, and Compose recomposes the UI that reads that state.

```kotlin
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }

    Column {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}
```

Good default principle:

> Keep UI as a function of state, hoist state when multiple composables need it, and keep side effects out of the rendering path.

---

## 2. Core layout primitives

### `Column`

Vertical stacking.

```kotlin
Column(
    modifier = Modifier.fillMaxSize(),
    verticalArrangement = Arrangement.Center,
    horizontalAlignment = Alignment.CenterHorizontally
) {
    Text("Title")
    Button(onClick = {}) { Text("Click") }
}
```

Key params:

```kotlin
verticalArrangement = Arrangement.Top / Center / Bottom / SpaceBetween / spacedBy(8.dp)
horizontalAlignment = Alignment.Start / CenterHorizontally / End
```

### `Row`

Horizontal stacking.

```kotlin
Row(
    modifier = Modifier.fillMaxWidth(),
    horizontalArrangement = Arrangement.SpaceBetween,
    verticalAlignment = Alignment.CenterVertically
) {
    Text("Left")
    Text("Right")
}
```

Key params:

```kotlin
horizontalArrangement = Arrangement.Start / Center / End / SpaceBetween / spacedBy(8.dp)
verticalAlignment = Alignment.Top / CenterVertically / Bottom
```

### `Box`

Overlay / stacking / corner alignment.

```kotlin
Box(
    modifier = Modifier.fillMaxSize()
) {
    Text(
        "Top start",
        modifier = Modifier.align(Alignment.TopStart)
    )

    Button(
        onClick = {},
        modifier = Modifier.align(Alignment.BottomCenter)
    ) {
        Text("Continue")
    }
}
```

Use `Box` when you need something in a corner, centered, or overlaid on top of something else.

---

## 3. Modifier order is critical

Modifier order changes the result. Modifiers are applied in sequence, and each modifier wraps the result of the next ones.

### Padding before background vs after background

```kotlin
Text(
    "Hello",
    modifier = Modifier
        .background(Color.Yellow)
        .padding(16.dp)
)
```

The background is applied before padding, so the yellow background is around the content and the padding creates space inside that decorated area.

```kotlin
Text(
    "Hello",
    modifier = Modifier
        .padding(16.dp)
        .background(Color.Yellow)
)
```

The padding is applied first, then the background is applied to the padded layout.

### Click area example

```kotlin
Modifier
    .clickable { }
    .padding(16.dp)
```

The click target is based on the area before padding.

```kotlin
Modifier
    .padding(16.dp)
    .clickable { }
```

The click target includes the padded area.

Important nuance for full-width rows:

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

This is often a good row pattern because `fillMaxWidth()` defines the large clickable area, `clickable` applies to that full-width area, and `padding` controls the internal content inset.

Useful rule:

> Put `clickable` after the modifiers that define the area you want clickable, and before modifiers that are only internal visual spacing.

---

## 4. Size, fill, wrap, required size

Common size modifiers:

```kotlin
Modifier.fillMaxSize()
Modifier.fillMaxWidth()
Modifier.fillMaxHeight()

Modifier.size(48.dp)
Modifier.width(120.dp)
Modifier.height(48.dp)

Modifier.wrapContentSize()
Modifier.defaultMinSize(minWidth = 48.dp, minHeight = 48.dp)
```

Useful patterns:

```kotlin
Button(
    modifier = Modifier
        .fillMaxWidth()
        .height(56.dp),
    onClick = {}
) {
    Text("Submit")
}
```

```kotlin
Icon(
    imageVector = Icons.Default.Search,
    contentDescription = null,
    modifier = Modifier.size(24.dp)
)
```

### `size` vs `requiredSize`

```kotlin
Modifier.size(100.dp)
```

Requests size while respecting parent constraints.

```kotlin
Modifier.requiredSize(100.dp)
```

Forces size more aggressively. Use rarely.

---

## 5. Weight in `Row` / `Column`

Use `weight` to divide remaining space.

```kotlin
Row(Modifier.fillMaxWidth()) {
    Text(
        "Left",
        modifier = Modifier.weight(1f)
    )
    Text("Right")
}
```

Common form row:

```kotlin
Row(
    modifier = Modifier.fillMaxWidth(),
    verticalAlignment = Alignment.CenterVertically
) {
    Text(
        "Name",
        modifier = Modifier.width(80.dp)
    )

    TextField(
        value = name,
        onValueChange = { name = it },
        modifier = Modifier.weight(1f)
    )
}
```

In a `Column`:

```kotlin
Column(Modifier.fillMaxSize()) {
    LazyColumn(
        modifier = Modifier.weight(1f)
    ) {
        items(messages) { message ->
            Text(message)
        }
    }

    MessageInput()
}
```

This is a classic chat-style layout: list takes remaining space, input stays at the bottom.

---

## 6. Alignment nuances

### Parent-level alignment

```kotlin
Column(
    horizontalAlignment = Alignment.CenterHorizontally
) {
    Text("Centered horizontally")
}
```

### Child-level alignment

```kotlin
Column {
    Text(
        "Only this child is centered",
        modifier = Modifier.align(Alignment.CenterHorizontally)
    )
}
```

### In `Box`

```kotlin
Box(Modifier.fillMaxSize()) {
    Text(
        "Bottom end",
        modifier = Modifier.align(Alignment.BottomEnd)
    )
}
```

Remember:

```kotlin
Column -> horizontalAlignment + verticalArrangement
Row    -> verticalAlignment + horizontalArrangement
Box    -> child Modifier.align(...)
```

---

## 7. `offset` vs `padding`

### `padding`

Affects measurement/layout space.

```kotlin
Modifier.padding(top = 16.dp)
```

### `offset`

Moves the composable visually after layout.

```kotlin
Modifier.offset(x = 8.dp, y = 4.dp)
```

Use `padding` for normal spacing. Use `offset` for badges, animations, and small visual nudges.

Example badge:

```kotlin
Box {
    Icon(Icons.Default.Notifications, contentDescription = null)

    Box(
        modifier = Modifier
            .size(8.dp)
            .align(Alignment.TopEnd)
            .offset(x = 2.dp, y = (-2).dp)
            .background(Color.Red, CircleShape)
    )
}
```

---

## 8. Spacing

Use `Arrangement.spacedBy` instead of manually putting `Spacer`s everywhere.

```kotlin
Column(
    verticalArrangement = Arrangement.spacedBy(12.dp)
) {
    Text("A")
    Text("B")
    Text("C")
}
```

Use `Spacer` when you need flexible space:

```kotlin
Row(Modifier.fillMaxWidth()) {
    Text("Left")
    Spacer(Modifier.weight(1f))
    Text("Right")
}
```

---

## 9. State: `remember`, `rememberSaveable`, hoisting

### Local UI state

```kotlin
var expanded by remember { mutableStateOf(false) }
```

Survives recomposition, but not activity/process recreation.

### Saveable state

```kotlin
var text by rememberSaveable { mutableStateOf("") }
```

Use for text input, selected tab, expanded/collapsed state, and simple UI state that should survive configuration changes.

### Hoisted state

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

State hoisting means replacing internal state with a `value` and event callback such as `onValueChange`.

Default rule:

> If only one composable cares, keep state local. If siblings need it, hoist to their lowest common parent. If business logic needs it, use a ViewModel or state holder.

---

## 10. Text input

Classic value-based `TextField`:

```kotlin
var text by rememberSaveable { mutableStateOf("") }

TextField(
    value = text,
    onValueChange = { text = it },
    label = { Text("Name") },
    singleLine = true,
    modifier = Modifier.fillMaxWidth()
)
```

Password:

```kotlin
var password by rememberSaveable { mutableStateOf("") }

TextField(
    value = password,
    onValueChange = { password = it },
    label = { Text("Password") },
    visualTransformation = PasswordVisualTransformation(),
    keyboardOptions = KeyboardOptions(
        keyboardType = KeyboardType.Password
    ),
    singleLine = true
)
```

Value-based `TextField(value, onValueChange)` is still common and simple. Newer Material 3 APIs also include state-based text fields.

---

## 11. Lists: `LazyColumn`

Use for scrollable lists.

```kotlin
LazyColumn(
    modifier = Modifier.fillMaxSize(),
    contentPadding = PaddingValues(16.dp),
    verticalArrangement = Arrangement.spacedBy(8.dp)
) {
    items(items) { item ->
        Text(item.name)
    }
}
```

With stable keys:

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

Use keys when list items can be inserted, removed, or reordered.

### Remember list state

```kotlin
val listState = rememberLazyListState()

LazyColumn(state = listState) {
    items(messages) { message ->
        Text(message.text)
    }
}
```

Scroll programmatically:

```kotlin
val scope = rememberCoroutineScope()

Button(
    onClick = {
        scope.launch {
            listState.animateScrollToItem(0)
        }
    }
) {
    Text("Top")
}
```

---

## 12. Effects

Effects are for work that should happen because of composition, but is not itself UI rendering.

### `LaunchedEffect`

Use for suspend work tied to composition.

```kotlin
LaunchedEffect(userId) {
    viewModel.loadUser(userId)
}
```

Important nuance:

```kotlin
LaunchedEffect(Unit) {
    // Runs once for this composable instance
}
```

```kotlin
LaunchedEffect(query) {
    // Cancels and restarts whenever query changes
}
```

### `rememberCoroutineScope`

Use when launching work from an event handler.

```kotlin
val scope = rememberCoroutineScope()

Button(
    onClick = {
        scope.launch {
            snackbarHostState.showSnackbar("Saved")
        }
    }
) {
    Text("Save")
}
```

Rule of thumb:

```kotlin
LaunchedEffect(...)      // start because composable appeared or key changed
rememberCoroutineScope() // start because user clicked/swiped/etc.
```

### `DisposableEffect`

Use when you need cleanup.

```kotlin
DisposableEffect(lifecycleOwner) {
    val observer = LifecycleEventObserver { _, event ->
        // observe lifecycle
    }

    lifecycleOwner.lifecycle.addObserver(observer)

    onDispose {
        lifecycleOwner.lifecycle.removeObserver(observer)
    }
}
```

### `rememberUpdatedState`

Use when an effect should not restart, but should call the latest callback.

```kotlin
val latestOnTimeout by rememberUpdatedState(onTimeout)

LaunchedEffect(Unit) {
    delay(1000)
    latestOnTimeout()
}
```

### `derivedStateOf`

Use for derived values that should only update when inputs meaningfully change.

```kotlin
val showButton by remember {
    derivedStateOf {
        listState.firstVisibleItemIndex > 0
    }
}
```

Good for scroll-derived UI.

### `snapshotFlow`

Use to convert Compose state reads into a Flow.

```kotlin
LaunchedEffect(listState) {
    snapshotFlow { listState.firstVisibleItemIndex }
        .collect { index ->
            // react to scroll index
        }
}
```

---

## 13. Clicks and gestures

For normal clicks, prefer high-level modifiers.

```kotlin
Modifier.clickable {
    // handle click
}
```

High-level modifiers like `clickable` include useful behavior such as accessibility support and visual feedback.

Long click:

```kotlin
Modifier.combinedClickable(
    onClick = {},
    onLongClick = {}
)
```

Tap detection:

```kotlin
Modifier.pointerInput(Unit) {
    detectTapGestures(
        onTap = { offset ->
            // offset is tap position
        },
        onLongPress = {}
    )
}
```

Drag:

```kotlin
var offsetX by remember { mutableStateOf(0f) }

Box(
    modifier = Modifier
        .offset { IntOffset(offsetX.roundToInt(), 0) }
        .pointerInput(Unit) {
            detectDragGestures { change, dragAmount ->
                change.consume()
                offsetX += dragAmount.x
            }
        }
)
```

---

## 14. Drawing and custom visuals

Use drawing modifiers when you do not need a full custom composable.

```kotlin
Box(
    modifier = Modifier
        .size(80.dp)
        .drawBehind {
            drawCircle(
                color = Color.Red,
                radius = size.minDimension / 2
            )
        }
)
```

Use `Canvas` when drawing is the main content.

```kotlin
Canvas(
    modifier = Modifier.size(120.dp)
) {
    drawCircle(
        color = Color.Blue,
        radius = size.minDimension / 2
    )
}
```

### `drawBehind` vs `drawWithContent`

```kotlin
Modifier.drawBehind {
    // draw before content
}
```

```kotlin
Modifier.drawWithContent {
    drawContent()
    // draw after content
}
```

Example overlay:

```kotlin
Modifier.drawWithContent {
    drawContent()
    drawRect(
        color = Color.Black.copy(alpha = 0.2f)
    )
}
```

---

## 15. Clipping, background, border, shape

Common card-like UI:

```kotlin
Box(
    modifier = Modifier
        .clip(RoundedCornerShape(16.dp))
        .background(MaterialTheme.colorScheme.surfaceVariant)
        .border(
            width = 1.dp,
            color = MaterialTheme.colorScheme.outline,
            shape = RoundedCornerShape(16.dp)
        )
        .padding(16.dp)
) {
    Text("Card")
}
```

Important: order matters.

Usually:

```kotlin
clip -> background -> border -> padding
```

Or:

```kotlin
Modifier.background(
    color = MaterialTheme.colorScheme.surfaceVariant,
    shape = RoundedCornerShape(16.dp)
)
```

Instead of separate `clip` when child clipping is not required:

```kotlin
Modifier.background(
    color = MaterialTheme.colorScheme.surfaceVariant,
    shape = RoundedCornerShape(16.dp)
)
```

If child content must also be clipped to the shape, use `clip`.

---

## 16. Animations

Common simple animation:

```kotlin
val alpha by animateFloatAsState(
    targetValue = if (visible) 1f else 0f,
    label = "alpha"
)

Box(
    modifier = Modifier.alpha(alpha)
)
```

Size/color/etc.:

```kotlin
val size by animateDpAsState(
    targetValue = if (expanded) 200.dp else 80.dp,
    label = "size"
)
```

Content enter/exit:

```kotlin
AnimatedVisibility(visible = expanded) {
    Text("Details")
}
```

Switching content:

```kotlin
AnimatedContent(
    targetState = selectedTab,
    label = "tab"
) { tab ->
    Text("Selected: $tab")
}
```

---

## 21. Mini practice problems

### Problem 1: Todo list

Build:

```text
TextField
Add button
LazyColumn of todos
Click todo to toggle done
Delete button per row
Empty state
```

Skills covered: state, list, row layout, click handling.

### Problem 2: Search/filter list

Build:

```text
Search TextField
List of hardcoded contacts
Filter as user types
Show "No results"
```

Skills covered: derived UI state, input, lazy list.

### Problem 3: Timer

Build:

```text
Start / pause / reset
Text showing elapsed seconds
LaunchedEffect loop
```

Skills covered: effects, coroutine cancellation, state.

### Problem 4: Drag card

Build:

```text
A box/card that can be dragged horizontally
Animate it back to center on release
```

Skills covered: pointer input, offset, animation.

---

## 22. Fast Compose API memory map

```kotlin
// Layout
Column
Row
Box
Spacer
LazyColumn
LazyRow

// Size
fillMaxSize()
fillMaxWidth()
size()
height()
width()
weight()

// Position
padding()
offset()
align()
Arrangement.spacedBy()
Arrangement.SpaceBetween
Alignment.Center
Alignment.CenterVertically
Alignment.CenterHorizontally

// Style
background()
clip()
border()
alpha()
shadow()

// State
remember
rememberSaveable
mutableStateOf
derivedStateOf

// Effects
LaunchedEffect
DisposableEffect
SideEffect
rememberCoroutineScope
rememberUpdatedState
snapshotFlow

// Input
TextField
Button
IconButton
Checkbox
Switch
clickable
pointerInput

// List
LazyColumn
items(...)
rememberLazyListState()

// Drawing
Canvas
drawBehind
drawWithContent
drawWithCache

// Animation
animateDpAsState
animateFloatAsState
AnimatedVisibility
AnimatedContent
updateTransition
```

---

## 23. Useful engineering notes

Use these principles when building Compose screens:

> “First model the screen state, then build composables around that state.”

> “If state only affects one UI element, keep it local with `rememberSaveable`.”

> “If state is shared by multiple composables, hoist it to the lowest common parent.”

> “Use `LazyColumn` instead of `Column.verticalScroll` for lists that can grow.”

> “Add stable keys when rows can be inserted, removed, or reordered.”

> “Use `LaunchedEffect(key)` when work should restart after that key changes.”

> “Use `rememberCoroutineScope` when a coroutine starts from a user event.”

> “Check modifier order when dealing with padding, click targets, background, clipping, and size.”
