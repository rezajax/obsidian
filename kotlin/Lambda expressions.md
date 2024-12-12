Kotlin allows you to write even more concise code for functions by using lambda expressions.

For example, the following `uppercaseString()` function:

```kotlin
fun uppercaseString(text: String): String {
    return text.uppercase()
}
fun main() {
    println(uppercaseString("hello"))
    // HELLO
}
```

Can also be written as a lambda expression:
```kotlin
fun main() {
    val upperCaseString = { text: String -> text.uppercase() }
    println(upperCaseString("hello"))
    // HELLO
}
```


### Pass to another function﻿[](https://kotlinlang.org/docs/kotlin-tour-functions.html#pass-to-another-function)

A great example of when it is useful to pass a lambda expression to a function, is using the [`.filter()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/filter.html) function on collections:

```kotlin 
fun main() {
    val numbers = listOf(1, -2, 3, -4, 5, -6)


    val positives = numbers.filter ({ x -> x > 0 })

    val isNegative = { x: Int -> x < 0 }
    val negatives = numbers.filter(isNegative)

    println(positives)
    // [1, 3, 5]
    println(negatives)
    // [-2, -4, -6]

}
```

>[!info]
>If a lambda expression is the only function parameter, you can drop the function parentheses `()`:
>```kotlin
>val positives = numbers.filter { x -> x > 0 }
>```
>> This is an example of a [trailing lambda](https://kotlinlang.org/docs/kotlin-tour-functions.html#trailing-lambdas), which is discussed in more detail at the end of this chapter.


