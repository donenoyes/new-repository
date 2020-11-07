```kotlin
fun observe() {
    events.observe(lifecycleOwner) { event ->
        showToast(event)
    }
}
```
