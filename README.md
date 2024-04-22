# Kotlin Multiplatform + Compose cheatsheet

## What is Compose?
Compose is a modern toolkit for building native Android UI. It simplifies and accelerates UI development.

- It's `functions` (CamelCase style!).
- Composable accept parameters.
- Use `MutableState` and `remember` to manage state.
- It can run parallel, run frequently, and run in any order.
- Can be skipped (if not visible, don't need to be recomposed).

## Useful tools / links
### Testing
- Test toolkit: [kotest](https://kotest.io/) - [How to use](https://test-architect.dev/junit-5-vs-kotest-part-1/)

### DI
- [decompose](https://github.com/arkivanov/Decompose)
- [voyager](https://github.com/adrielcafe/voyager)

### Code quality / linters
- [konsist](https://docs.konsist.lemonappdev.com/) - [samples](https://docs.konsist.lemonappdev.com/inspiration/starter-projects)
- [detekt](https://detekt.dev/docs/intro)
- [ktlint](https://pinterest.github.io/ktlint/latest/)
- [ktlint-compose-rules](https://mrmans0n.github.io/compose-rules/ktlint/)
- [danger](https://danger.systems/kotlin/)
- [spotless]()

### Helpers
- [acompanist](https://github.com/google/accompanist) - Android only? - [permissions](https://github.com/google/accompanist/blob/main/permissions), [navigation](https://github.com/google/accompanist/blob/main/navigation-material), [adaptive screens](https://google.github.io/accompanist/adaptive/)

### Networking
- [ktor](https://ktor.io/docs/client-create-multiplatform-application.html)
- [ktorfit](https://foso.github.io/Ktorfit/)

### Database
- [sqldelight](https://cashapp.github.io/sqldelight/)

### Resources / L10n / I18n
- [Moko](https://moko.icerock.dev/) (resources, geo, permissions, etc)
- [lyricist](https://github.com/adrielcafe/lyricist) resources L10n

### iOS setup
- [SKIE](https://skie.touchlab.co/)


## Setting project

<details>
<summary>.editorconfig</summary>

```ini
root = true

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

#Compose
ktlint_function_naming_ignore_when_annotated_with=Composable, Test

[*.md]
trim_trailing_whitespace = false
max_line_length = unset
```
</details>

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

#### Remember state
```kotlin
@Composable
fun ViewName(item: Item) {
    val checkedState: Item? by rememberSaveable { mutableStateOf(null) }

    Checkbox(checked = { checkedState == item })
}
```
