```python
// write
private val emitter: EventEmitter<String> = EventEmitter()
val events: EventSource<String> = emitter

fun doSomething() {
    emitter.emit("hello")
}

// read
fun observe() {
    events.observe(lifecycleOwner) { event ->
        showToast(event)
    }
}
```
