# Kotlin Multiplatform + Compose cheatsheet

This cheat sheet is primarily focused on the Jetpack Compose part of Android plus on the Kotlin Multiplatform projects.
So, not all described can be used for multiplatform projects, but most of them can be used in Android projects based on KMM + Compose.
It's a good start for multiplatform projects when we migrate existing Android projects to KMM.

## What is Compose?

Compose is a modern toolkit for building native Android UI. It simplifies and accelerates UI development.

- It's `functions` (CamelCase style!).
- Composable accept parameters.
- Use `MutableState` and `remember` to manage state.
- It can run parallel, run frequently, and run in any order.
- Can be skipped (if not visible, don't need to be recomposed).

## Useful tools / links

### Guidelines

- [Compose guidelines](https://developer.android.com/develop/ui/compose/api-guidelines)
- [API Guidelines for Jetpack Compose](https://android.googlesource.com/platform/frameworks/support/+/androidx-main/compose/docs/compose-api-guidelines.md)
- [API Guidelines for `@Composable` components in Jetpack Compose](https://android.googlesource.com/platform/frameworks/support/+/androidx-main/compose/docs/compose-component-api-guidelines.md)
- [Kotlin for Compose](https://developer.android.com/develop/ui/compose/kotlin)

### Basic links

- [Jetpack Compose (Google)](https://developer.android.com/jetpack/compose)
- [Compose samples (Google)](https://developer.android.com/jetpack/compose/samples)
- [Compose codelabs (Google)](https://developer.android.com/codelabs/jetpack-compose-basics)
- [Compose documentation (Google)](https://developer.android.com/jetpack/compose/documentation)
- [Compose samples (Google)](https://github.com/android/compose-samples)


- [Composables](https://www.composables.com/)


- [Kotlin Multiplatform](https://www.jetbrains.com/help/kotlin-multiplatform-dev/get-started.html)


- [Compose playground](https://foso.github.io/Jetpack-Compose-Playground/)


- [Android interview questions](https://github.com/amitshekhariitbhu/android-interview-questions)

### Codelabs

- [Android courses](https://developer.android.com/courses)
- [Compose courses](https://developer.android.com/courses/jetpack-compose/course)
- [Google Developers codelabs](https://developers.google.com/learn?text=compose)

### Interesting/sample projects

- [JetBrains KMM samples](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-samples.html)
- [TV maniac](https://github.com/thomaskioko/tv-maniac?tab=readme-ov-file)

### Design

- [Material Theme Builder](https://material-foundation.github.io/material-theme-builder/)

### K2

- [Benchmark](https://blog.jetbrains.com/kotlin/2024/04/k2-compiler-performance-benchmarks-and-how-to-measure-them-on-your-projects/), [github](https://github.com/Kotlin/k2-performance-metrics)

### Testing

- Test toolkit: [kotest](https://kotest.io/) - [How to use](https://test-architect.dev/junit-5-vs-kotest-part-1/)

### DI

- [decompose](https://github.com/arkivanov/Decompose)
- [voyager](https://github.com/adrielcafe/voyager)
- [kotlin-inject](https://github.com/evant/kotlin-inject)

### Code style / quality / linters

- [konsist](https://docs.konsist.lemonappdev.com/) - [samples](https://docs.konsist.lemonappdev.com/inspiration/starter-projects)
- [detekt](https://detekt.dev/docs/intro)
- [ktlint](https://pinterest.github.io/ktlint/latest/)
- [ktlint-compose-rules](https://mrmans0n.github.io/compose-rules/ktlint/)
- [danger](https://danger.systems/kotlin/)

### Helpers

- [acompanist](https://github.com/google/accompanist) - Android
  only? - [permissions](https://github.com/google/accompanist/blob/main/permissions), [navigation](https://github.com/google/accompanist/blob/main/navigation-material), [adaptive screens](https://google.github.io/accompanist/adaptive/)

### Networking

- [ktor](https://ktor.io/docs/client-create-multiplatform-application.html)
- [ktorfit](https://foso.github.io/Ktorfit/)

### Database

- [sqldelight](https://cashapp.github.io/sqldelight/)
- [Room](https://developer.android.com/jetpack/androidx/releases/room#2.7.0-alpha01) from 2.7.0-alpha01
- [DataStore](https://developer.android.com/jetpack/androidx/releases/datastore#1.1.1) from 1.1.0

### Resources / L10n / I18n

- [JetBrains Compose resources](https://www.jetbrains.com/help/kotlin-multiplatform-dev/compose-images-resources.html)
- [Moko](https://moko.icerock.dev/) (resources, geo, permissions, etc)
- [lyricist](https://github.com/adrielcafe/lyricist) resources L10n

### UI

- Image loader: [coil](https://coil-kt.github.io/coil/compose/) (Coil 3 is KMM ready)

### Logging

- [kermit](https://kermit.touchlab.co/docs/)
- [napier](https://github.com/AAkira/Napier)

### iOS setup

- [SKIE](https://skie.touchlab.co/)

### Wear OS

- [Horologist](https://github.com/google/horologist) bundle of libraries for Wear OS

## Setting project

<details>
<summary>.editorconfig</summary>

```ini
# We can use global .editorconfig file for personal (all projects) settings.
# https://blog.danskingdom.com/Reasons-to-use-both-a-local-and-global-editorconfig-file/
root = false

[*]
indent_style = space
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.{kt,kts}]
max_line_length = 140
indent_size = 4

# Don't allow any wildcard imports
ij_kotlin_packages_to_use_import_on_demand = unset

# Prevent wildcard imports
ij_kotlin_name_count_to_use_star_import = 99
ij_kotlin_name_count_to_use_star_import_for_members = 99

ij_kotlin_allow_trailing_comma = true
ij_kotlin_allow_trailing_comma_on_call_site = true

ktlint_code_style = ktlint_official
ktlint_standard = enabled

# Compose
ktlint_function_naming_ignore_when_annotated_with=Composable, Test

[*.md]
trim_trailing_whitespace = false
max_line_length = unset
```

</details>

## Preview

Use `annotation class` to create a preview.

```kotlin
@Preview(
    name = "Light Mode",
    group = "Light / dark mode",
    uiMode = Configuration.UI_MODE_NIGHT_NO
)
@Preview(
    name = "Dark Mode",
    group = "Light / dark mode",
    uiMode = Configuration.UI_MODE_NIGHT_YES
)
annotation class PreviewLightDarkMode
```

Usage:

```kotlin
@PreviewFotnScale
@PreviewLightDarkMode
@Composable
fun SomePreview() {
    ...
}
```

Will create both preview just by annotating the function. We can create same for font size, etc..

## Components

### Surface

Used to apply a background color, shape, border, elevation, etc. to a composable function.
Text color will be used as `on[Surface]` color when we use `MaterialTheme.colorScheme.surface`.

### Scaffold

Used to create a layout with a top bar, bottom bar, and a body.
Solve issues with drawing under status bar, navigation bar, etc.
Just provide padding to child composable.

```kotlin
Scaffold(modifier) { paddingValues ->
    Surface(modifier = modifier.padding(paddingValues)) {
        ...
    }
```

### Column

Used to create a vertical layout.

### Row

Used to create a horizontal layout.

### LazyColumn

We can [save scroll position / state](https://developer.android.com/develop/ui/compose/lists#react-to-scroll-position) by using `rememberLazyListState()`.

```kotlin
@Composable
fun LazyColumnList() {
    val state: LazyListState = rememberLazyListState()

    LazyColumn(state = state) {
        items(items)
    }
}
```

#### Remember state

`remembered` is used to remember the state of a composable function.
It is used to store the state of a composable function and recompose the composable function when the state changes.

```kotlin
@Composable
fun ViewName(item: Item) {
    val checkedState: MutableState<Item?> = remembered {
        mutableStateOf(null)
    }

    Checkbox(checked = { checkedState.value == item })
}
```

Don't use `=`, use `by` keyword instead (not need call it with `.value`).

```kotlin
@Composable
fun ViewName(item: Item) {
    var checkedState: MutableState<Item?> by remembered {
        mutableStateOf(null)
    }

    Checkbox(
        checked = { checkedState == item },
        onCheckedChange = { checkedState = it }
    )
}
```

Use `remember` to retain the state across recompositions.

We can go with the `rememberSaveable` to retain the state across configuration changes, but due to the limitation with the data type compatibility (which can be solved with some boilerplate code),
better to use ViewModel.

```kotlin
@Composable
fun ViewName(item: Item) {
    val checkedState: Item? by rememberSaveable { mutableStateOf(null) }

    Checkbox(checked = { checkedState == item })
}
```

Remember can store lists as well. But don't store it by adding items to the list, use `mutableStateOf` instead.
In case, that we call `list.addAll()` on remembered list, it can duplicate items or call recomposition multiple times and have performance issues.

```kotlin
val list = remember {
    mutableStateListOf<Item>().apply { addAll(getAllTasks()) }
}
```

#### [Animations](https://developer.android.com/develop/ui/compose/animation/introduction)

How to [choose proper animation](https://developer.android.com/develop/ui/compose/animation/choose-api) type.

![](https://developer.android.com/static/develop/ui/compose/images/animations/compose_animation_decision_tree_v2.jpg)

[Animated graph / chart](https://youtu.be/1yiuxWK74vI?si=UUIEIhwJYrthUSL-)

Use `animate[Dp|Size|Offset|*]AsState`.Animation is interruptible (can be cancelled by new animation).

``` kotlin
val extraPadding by animateDpAsState(
    if (expanded) 48.dp else 0.dp
)

```

Expand / collapse animation for show items
```kotlin
AnimatedVisibility(
    visible = expanded
) {
    // content
    TextView()
}
```

Expand / collapse same item (for example maxLines for Text item)
```kotlin
var expanded = remember { mutableStateOf(false) }
Text(
    text = "Some\nmultiline\ntext",
    maxLines = if (expanded) Int.MAX_VALUE else 1,
    overflow = TextOverflow.Ellipsis,
    modifier = Modifier
        .animateContentSize()
        .clickable { expanded = !expanded }
)
```

Animate content changes
```kotlin
AnimatedContent(
    targetState = content,
    transitionSpec = {
        fadeIn(animationSpec = tween(300))
        slideIntoContainer(animationSpec = ..., towards = Up).with(slideOutOfContainer(..., towards = Down))
    }
 ) { targetState ->
    when(targetState) {
        State.Screen1 -> Screen1()
        State.Screen2 -> Screen2()
    }
}
```

Animate progress bar
```kotlin
val progress by animateFloatAsState(
    targetValue = currentProgress / totalProgress.toFloat(),
)

LinearProgressIndicator(progress = progress)
```

Animate rotation (like background around image)
```kotlin
val infiniteTransition = rememberInfiniteTransition()
val rotateAnimation = infiniteTransition.animateFloat(
    initialValue = 0f,
    targetValue = 360f,
    animationSpec = infiniteRepeatable(
        animation = tween(1000, easing = LinearEasing),
        easing = LinearEasing
    )
)

Image(
    modifier = Modifier
        .drawBehind {
            rotate(rotateAnimation.value) {
                drawCircle(rainbowColorBrush, style = Stroke(borderWidth))
            }
        }
        .padding(borderWidth)
        .clip(CircleShape)
    
)
```

#### [Shapes](https://m3.material.io/styles/shape/overview)
```kotlin
    modifier = modifier
        .background(MaterialTheme.colorScheme.background, shape = CircleShape) // for search bars, icons, etc... circle whole item
        .background(MaterialTheme.colorScheme.background, shape = MaterialTheme.shapes.medium) // rounded corners
)
```

Gradient cut border shape for inputs, etc...
```kotlin
val Gradient = listOf(...)
Modifier
    .border(
        border = BorderStroke(
            width = 2.dp,
            brush = Brush.linearGradient(Gradient)
        ),
        shape = CutCornerShape(8.dp)
    )
```

Gradient for cursor while typing in input field.
```kotlin
val Gradient = listOf(...)
        
BasicTextField(
    cursorBrush = Brush.linearGradient(Gradient)
```

#### [Typography](https://m3.material.io/styles/typography/overview)
