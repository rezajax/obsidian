
> [!Warning]
> با class و بی کلاس مسعله این است.!

```kotlin
class Contact(val id: Int, var email: String)

fun main() {
    val contact = Contact(1, "mary@gmail.com")
    println(contact.email)
}
```


اگه نخواهیم از class استفاده کنیم!

If you'd like to create an object similar to Contact without using a class, you can use a data structure like a Map or data class to hold the data. Here's how you can achieve that:

### 1. Using a function with a `Map`:

You can use a `Map` to represent the contact details.

```kotlin
fun createContact(id: Int, email: String): Map<String, Any> {
    return mapOf("id" to id, "email" to email)
}

fun main() {
    val contact = createContact(1, "mary@gmail.com")
    println(contact["email"]) // Output: mary@gmail.com
}
```

### 2. Using a lambda to create an object-like structure:

You can also use the `apply` function or a similar approach to initialize a `Map` in a more inline fashion.

```kotlin
fun main() {
    val contact = mutableMapOf<String, Any>().apply {
        put("id", 1)
        put("email", "mary@gmail.com")
    }
    println(contact["email"]) // Output: mary@gmail.com
}

```
These approaches avoid using a class while still providing a way to represent and store data like in the original `Contact` example.

### Data Holder

If you want to have an output like `println(contact.email)` without using a class, you can create a custom **data holder** using a **data class** or a **lambda** with property access syntax. However, if you truly want to avoid using a class, the best approach would be to use a `Map` and make it behave like an object.

Here’s how you can do it:

### Using `Map` and extension properties:

You can extend the `Map` with properties to allow access like a class.

```kotlin
fun createContact(id: Int, email: String): Map<String, Any> {
    return mapOf("id" to id, "email" to email)
}

val Map<String, Any>.email: String
    get() = this["email"] as String

fun main() {
    val contact = createContact(1, "mary@gmail.com")
    println(contact.email) // Output: mary@gmail.com
}

```
### Explanation:

- We use a `Map<String, Any>` to store the `Contact` data.
- We create an **extension property** `email` for the `Map`, which allows us to access the value like a class property (`contact.email`).

This allows you to simulate the class-like behavior while avoiding the use of a formal `class`.


---

### Trailing commas﻿[](https://kotlinlang.org/docs/coding-conventions.html#trailing-commas)

کاماهای دنباله دار، کامای انتها

A trailing comma is a comma symbol after the last item in a series of elements:

```kotlin
class Person(
    val firstName: String,
    val lastName: String,
    val age: Int, // trailing comma
)
```



