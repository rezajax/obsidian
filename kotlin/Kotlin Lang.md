---
tags:
  - programming
Date: 2024-12-06
---
## Named arguments

#optional

For concise code, and does make your code easier to read

```kotlin
fun printMessageWithPrefix(message: String, prefix: String) {
    println("[$prefix] $message")
}

fun main() {
    // Uses named arguments with swapped parameter order
    printMessageWithPrefix(prefix = "Log", message = "Hello")
    // [Log] Hello
}
```

