
# when

> [!Success]
> رضا میگه من عاشق when هستم، و ب نظرم ساختارش خیلی جالبه.

![[Pasted image 20241215154020.png]]
```kotlin
fun main() {
    val x: Any = 20

    when (x) {
        2, 3, 5, 7 -> println("x is a prime number between 1 and 10.")
        in 1..10 -> println("x is a number between 1 and 10, but not a prime number.")
        is Int -> println("x is an integer number, but not between 1 and 10.")
        else -> println("x isn't an integer number.")
    }
}
```

Here's how you can write the Kotlin `when` example in Java using a combination of `if-else` and `switch` (Java doesn't have a direct equivalent of Kotlin's `when`):

```java
public class Main {
    public static void main(String[] args) {
        Object x = 20; // `Object` is the closest to Kotlin's `Any`

        if (x instanceof Integer) {
            int value = (Integer) x;

            switch (value) {
                case 2:
                case 3:
                case 5:
                case 7:
                    System.out.println("x is a prime number between 1 and 10.");
                    break;
                default:
                    if (value >= 1 && value <= 10) {
                        System.out.println("x is a number between 1 and 10, but not a prime number.");
                    } else {
                        System.out.println("x is an integer number, but not between 1 and 10.");
                    }
            }
        } else {
            System.out.println("x isn't an integer number.");
        }
    }
}

```

write simple equivalent in java
Here's a simpler equivalent of your Kotlin `when` statement in Java:

```java
public class Main {
    public static void main(String[] args) {
        Object x = 20; // Closest to Kotlin's `Any`

        if (x instanceof Integer) {
            int value = (Integer) x;
            if (value == 2 || value == 3 || value == 5 || value == 7) {
                System.out.println("x is a prime number between 1 and 10.");
            } else if (value >= 1 && value <= 10) {
                System.out.println("x is a number between 1 and 10, but not a prime number.");
            } else {
                System.out.println("x is an integer number, but not between 1 and 10.");
            }
        } else {
            System.out.println("x isn't an integer number.");
        }
    }
}

```

# Lambda

[https://developer.android.com/codelabs/basic-android-kotlin-compose-function-types-and-lambda?continue=https%3A%2F%2Fdeveloper.android.com%2Fcourses%2Fpathways%2Fandroid-basics-compose-unit-2-pathway-1%23codelab-https%3A%2F%2Fdeveloper.android.com%2Fcodelabs%2Fbasic-android-kotlin-compose-function-types-and-lambda#0](Link to this )

> [!success]
> فانکش ها ی نوع از داده هستن

As a first-class construct, **functions are also data types**, so you can store functions in variables, pass them to functions, and return them from functions. Perhaps you want the ability to change the behavior of a piece of your app at runtime or nest composable functions to build layouts like you did in previous codelabs. All this is made possible by lambda expressions.


> [!ABOUT]
to refer to a function as a value, you need to use the function reference operator `::` . The syntax is illustrated in this image

![[Pasted image 20241215160230.png]]

```kotlin
fun main() {
    val trickFunction = ::trick
}

fun trick() {
    println("No treats!")
}
```
## Redefine the function with a lambda expression

Lambda expressions provide a concise syntax to define a function without the `fun` keyword. You can store a lambda expression directly in a variable without a function reference on another function.
![[Pasted image 20241215161418.png]]
```kotlin
fun main() {
    val trickFunction = trick
    trick()
    trickFunction()
}

val trick = {
    println("No treats!")
}
```

