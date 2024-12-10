---
tags:
  - programming
Date: 2024-12-06
---
# hi
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

## Collections type :LiGroup:


Kotlin has the following collections for grouping items:

| Collection type | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| Lists           | Ordered collections of items                                            |
| Sets            | Unique unordered collections of items                                   |
| Maps            | Sets of key-value pairs where keys are unique and map to only one value |

Each collection type can be mutable or read only.


## List﻿[](https://kotlinlang.org/docs/kotlin-tour-collections.html#list)

Lists store items in the order that they are added, and allow for duplicate items.

```kotlin
fun main() { 
    // Read only list
    val readOnlyShapes = listOf("triangle", "square", "circle")
    println(readOnlyShapes)
    // [triangle, square, circle]

    // Mutable list with explicit type declaration
    val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
    println(shapes)
    // [triangle, square, circle]
}
```

with index 
```kotlin
fun main() {
	val readOnlyShapes = listOf("triangle", "square", "circle")  
	for ( it in readOnlyShapes.withIndex()) {  
	    println( "$it and ${it.index}") //can use it.value  
	}
}
```

## Set﻿[](https://kotlinlang.org/docs/kotlin-tour-collections.html#set)

Whereas lists are ordered and allow duplicate items, sets are unordered and only store unique items.

```kotlin
fun main() {
    // Read-only set
    val readOnlyFruit = setOf("apple", "banana", "cherry", "cherry")
    // Mutable set with explicit type declaration
    val fruit: MutableSet<String> = mutableSetOf("apple", "banana", "cherry", "cherry")

    println(readOnlyFruit)
    // [apple, banana, cherry]
}
```

> [!INFO]
> As sets are **unordered**, you can't access an item at a particular index.

### Exercise 2﻿[](https://kotlinlang.org/docs/kotlin-tour-collections.html#exercise-2)

You have a set of protocols supported by your server. A user requests to use a particular protocol. Complete the program to check whether the requested protocol is supported or not (`isSupported` must be a Boolean value).

```kotlin
fun main() {  
    val SUPPORTED = setOf("HTTP", "HTTPS", "FTP")  
    val requested = "smtp"  
    val isSupported = requested.uppercase() in SUPPORTED  
    println("Support for $requested: $isSupported")  
}
```

> [!Hint]
Make sure that you check the requested protocol in upper case. You can use the [`.uppercase()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/uppercase.html) function to help you with this.


## Map﻿[](https://kotlinlang.org/docs/kotlin-tour-collections.html#map)

Maps store items as key-value pairs. You access the value by referencing the key. You can imagine a map like a **food menu**. You can find the price (value), by finding the food (key) you want to eat. Maps are useful if you want to look up a value without using a numbered index, like in a list.

```kotlin
fun main() {
    // Read-only map
    val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
    println(readOnlyJuiceMenu)
    // {apple=100, kiwi=190, orange=100}

    // Mutable map with explicit type declaration
    val juiceMenu: MutableMap<String, Int> = mutableMapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
    println(juiceMenu)
    // {apple=100, kiwi=190, orange=100}
}
```




# Control Flow (conditional expressions)

### If﻿[](https://kotlinlang.org/docs/kotlin-tour-control-flow.html#if)

To use `if`, add the conditional expression within parentheses `()` and the action to take if the result is true within curly braces `{}`:

```kotlin
fun main() {
    val d: Int
    val check = true

    if (check) {
        d = 1
    } else {
        d = 2
    }

    println(d)
    // 1
}
```

There is no ternary operator `condition ? then : else` in Kotlin. Instead, `if` can be used as an expression. If there is only one line of code per action, the curly braces `{}` are optional:

```kotlin
fun main() { 
    val a = 1
    val b = 2

    println(if (a > b) a else b) // Returns a value: 2
}
```

### When﻿[](https://kotlinlang.org/docs/kotlin-tour-control-flow.html#when)

Use `when` when you have a conditional expression with multiple branches.

`when` can be used either as a statement or as an expression. A statement doesn't return anything but performs actions instead.
#### Statement

```kotlin
fun main() {
    val obj = "Hello"

    when (obj) {
        // Checks whether obj equals to "1"
        "1" -> println("One")
        // Checks whether obj equals to "Hello"
        "Hello" -> println("Greeting")
        // Default statement
        else -> println("Unknown")     
    }
    // Greeting
}
```

#### Expression
An expression returns a value that can be used later in your code.

Here is an example of using `when` as an expression. The `when` expression is assigned immediately to a variable which is later used with the `println()` function:
```kotlin
fun main() {
    val trafficLightState = "Red" // This can be "Green", "Yellow", or "Red"

    val trafficAction = when {
        trafficLightState == "Green" -> "Go"
        trafficLightState == "Yellow" -> "Slow down"
        trafficLightState == "Red" -> "Stop"
        else -> "Malfunction"
    }

    println(trafficAction)
    // Stop
}
```
However, you can have the same code but with `trafficLightState` as the subject:
```kotlin
fun main() {
    val trafficLightState = "Red" // This can be "Green", "Yellow", or "Red"

    val trafficAction = when (trafficLightState) {
        "Green" -> "Go"
        "Yellow" -> "Slow down"
        "Red" -> "Stop"
        else -> "Malfunction"
    }

    println(trafficAction)  
    // Stop
}
```
## Loops practice
Write a program that simulates the [Fizz buzz](https://en.wikipedia.org/wiki/Fizz_buzz) game. Your task is to print numbers from 1 to 100 incrementally, replacing any number divisible by three with the word "fizz", and any number divisible by five with the word "buzz". Any number divisible by both 3 and 5 must be replaced with the word "fizzbuzz".

```kotlin

Example solution
 {...}
fun main() {
    for (number in 1..100) {
        println(
            when {
                number % 15 == 0 -> "fizzbuzz"
                number % 3 == 0 -> "fizz"
                number % 5 == 0 -> "buzz"
                else -> "$number"
            }
        )
    }
}
```

My solution

```kotlin
fun main() {  
    for (i in 1..100) {  
        if (i % 3 == 0) println("Fizz")  
        if (i % 5 == 0) println("Buzz")  
        println(i)  
    }  
  
    for (i in 1..100)  
        if (i % 3 == 0) println("Fizz") else if (i % 5 == 0) println("Buzz") else println(i)  
  
    for (i in 0 until 100) {  
        when {  
            (i % 3 == 0) -> println("Fizz")  
            (i % 5 == 0) -> println("Buzz")  
            else -> println(i)  
        }  
    }  
}
```

### Exercise 3﻿[](https://kotlinlang.org/docs/kotlin-tour-control-flow.html#loops-exercise-3)

You have a list of words. Use `for` and `if` to print only the words that start with the letter `l`.
‍‍
```kotlin
fun main() {  
    val words = listOf("dinosaur", "limousine", "magazine", "language")  
  
    //kotl.in solotion  
    for (w in words)  
        if (w.startsWith("l"))  
            println(w)  
  
  
  
    for (word in words)  
        if (word.startsWith("l")) {println(word)}  
  
  
    println(words.filter { it.startsWith("l") })  
      
}
```

