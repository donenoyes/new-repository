```Kotlin
fun observe() {
    events.observe(lifecycleOwner) { event ->
        showToast(event)
    }
}
```
