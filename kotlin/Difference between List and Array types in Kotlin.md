

[](https://stackoverflow.com/posts/36263748/timeline)

[Arrays](https://kotlinlang.org/docs/reference/basic-types.html#arrays) and lists (represented by [`List<T>`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-list/) and its subtype [`MutableList<T>`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/index.html)) have many differences, here are the most significant ones:

- `Array<T>` is a class with known implementation: it's a sequential fixed-size memory region storing the items (and on JVM it is represented by [Java array](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html)).
    
    `List<T>` and `MutableList<T>` are interfaces which have different implementations: `ArrayList<T>`, `LinkedList<T>` etc. Memory representation and operations logic of lists are defined in concrete implementation, e.g. indexing in a `LinkedList<T>` goes through the links and takes O(n) time whereas `ArrayList<T>` stores its items in a dynamically allocated array.
    
    ```kotlin
    val list1: List<Int> = LinkedList<Int>()
    val list2: List<Int> = ArrayList<Int>()
    ```
    
- `Array<T>` is mutable (it can be changed through any reference to it), but `List<T>` doesn't have modifying methods (it is either [read-only view of `MutableList<T>`](https://stackoverflow.com/questions/34770493/kotlin-instantiate-immutable-list/34770659#34770659) or an [immutable list implementation](https://stackoverflow.com/questions/7713274/java-immutable-collections)).
    
    ```kotlin
    val a = arrayOf(1, 2, 3)
    a[0] = a[1] // OK
    
    val l = listOf(1, 2, 3)
    l[0] = l[1] // doesn't compile
    
    val m = mutableListOf(1, 2, 3)
    m[0] = m[1] // OK
    ```
    
- Arrays have fixed size and cannot expand or shrink retaining identity (you need to copy an array to resize it). As to the lists, `MutableList<T>` has `add` and `remove` functions, so that it can increase and reduce its size.
    
    ```kotlin
    val a = arrayOf(1, 2, 3)
    println(a.size) // will always be 3 for this array
    
    val l = mutableListOf(1, 2, 3)
    l.add(4)
    println(l.size) // 4
    ```
    
- `Array<T>` is [invariant on `T`](https://kotlinlang.org/docs/reference/generics.html#variance) (`Array<Int>` is not `Array<Number>`), the same for `MutableList<T>`, but `List<T>` is covariant (`List<Int>` is `List<Number>`).
    
    ```kotlin
    val a: Array<Number> = Array<Int>(0) { 0 } // won't compile
    val l: List<Number> = listOf(1, 2, 3) // OK
    ```
    
- Arrays are optimized for primitives: there are separate `IntArray`, `DoubleArray`, `CharArray` etc. which are mapped to Java primitive arrays (`int[]`, `double[]`, `char[]`), not [boxed](https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html) ones (`Array<Int>` is mapped to Java's `Integer[]`). Lists in general do not have implementations optimized for primitives, though some libraries (outside JDK) provide primitive-optimized lists.
    
- `List<T>` and `MutableList<T>` are [mapped types](https://kotlinlang.org/docs/reference/java-interop.html#mapped-types) and have special behaviour in Java interoperability (Java's `List<T>` is seen from Kotlin as either `List<T>` or `MutableList<T>`). Arrays are also mapped, but they have [other rules](https://kotlinlang.org/docs/reference/java-interop.html#java-arrays) of Java interoperability.
    
- Certain array types are used in [annotations](https://kotlinlang.org/docs/reference/annotations.html#annotations) (primitive arrays, `Array<String>`, and arrays with `enum class` entries), and there's a special [array literal syntax for annotations](https://kotlinlang.org/docs/reference/whatsnew12.html#array-literals-in-annotations). Lists and other collections cannot be used in annotations.
    
- As to the usage, good practice is to prefer using lists over arrays everywhere except for performance critical parts of your code, the reasoning is the same to [that for Java](http://www.javapractices.com/topic/TopicAction.do?Id=39).
- 
---

The major difference from usage side is that [Arrays](https://kotlinlang.org/docs/reference/basic-types.html#arrays) have a fixed size while [`(Mutable)List`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/index.html) can adjust their size dynamically. Moreover `Array` is mutable whereas `List` is not.

Furthermore [`kotlin.collections.List`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-list/index.html) is an interface implemented among others by `java.util.ArrayList`. It's also extended by `kotlin.collections.MutableList` to be used when a collection that allows for item modification is needed.

On the jvm level, `Array` is represented by [arrays](https://docs.oracle.com/javase/specs/jls/se7/html/jls-10.html). `List` on the other hand is represented by [`java.util.List`](https://docs.oracle.com/javase/7/docs/api/java/util/List.html) since there are no immutable collections equivalents available in Java.