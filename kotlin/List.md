# All List


> [!Warning]
> در Java، مجموعه‌های **immutable** به صورت پیش‌فرض وجود ندارند و باید از کلاس‌های خاصی استفاده کرد (مثل `Collections.unmodifiableList`):

| Collection type | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| Lists           | Ordered collections of items                                            |
| Sets            | Unique unordered collections of items                                   |
| Maps            | Sets of key-value pairs where keys are unique and map to only one value |
|                 |                                                                         |



## Example

### List
در Kotlin، می‌توان از توابع کمکی برای مقداردهی استفاده کرد: مثل listOf() و  mutableListOf()
```kotlin

val list = listOf("A", "B", "C")  // غیرقابل تغییر
mutableListOf("A", "B", "C")  // قابل تغییر`
```

در Kotlin، توابعی مثل `filter`، `map` و غیره به صورت داخلی و مستقیم قابل استفاده هستند:

```kotlin
val filteredList = list.filter { it.startsWith("A") }
```
### 