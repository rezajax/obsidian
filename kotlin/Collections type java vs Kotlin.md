### 1. **تعداد و تنوع Collection‌ها**

#### Java:

- مجموعه‌های اصلی در Java در قالب **`java.util`** تعریف شده‌اند.
- انواع اصلی:
    - **List** (مثل `ArrayList`, `LinkedList`)
    - **Set** (مثل `HashSet`, `TreeSet`)
    - **Map** (مثل `HashMap`, `TreeMap`)
- هر کدام از این مجموعه‌ها پیاده‌سازی‌های متعددی دارند که انتخاب مناسب آن‌ها پیچیدگی دارد.

#### Kotlin:

- Kotlin به صورت پیش‌فرض از مجموعه‌های Java استفاده می‌کند، اما یک **API ساده‌تر** برای آن‌ها فراهم کرده است.
- انواع اصلی:
    - **List**
    - **Set**
    - **Map**
- تمرکز Kotlin روی تفاوت بین مجموعه‌های **immutable** (غیرقابل تغییر) و **mutable** (قابل تغییر) است:
    - `List` → غیرقابل تغییر
    - `MutableList` → قابل تغییر
- تعداد و تنوع کلاس‌ها کمتر است و درک و استفاده از آن‌ها ساده‌تر است.

---

### 2. **ایجاد و مقداردهی اولیه**

#### Java:

ایجاد مجموعه‌ها در Java معمولاً به کد بیشتری نیاز دارد:

java

Copy code

`List<String> list = new ArrayList<>(); list.add("A"); list.add("B"); list.add("C");`

#### Kotlin:

در Kotlin، می‌توان از توابع کمکی برای مقداردهی استفاده کرد:

kotlin

Copy code

`val list = listOf("A", "B", "C")  // غیرقابل تغییر val mutableList = mutableListOf("A", "B", "C")  // قابل تغییر`

---

### 3. **کار با مجموعه‌ها (فیلتر کردن، نگاشت و غیره)**

#### Java:

کار با مجموعه‌ها معمولاً از طریق حلقه‌ها یا Stream API انجام می‌شود:

java

Copy code

`List<String> filteredList = list.stream()     .filter(item -> item.startsWith("A"))     .collect(Collectors.toList());`

#### Kotlin:

در Kotlin، توابعی مثل `filter`، `map` و غیره به صورت داخلی و مستقیم قابل استفاده هستند:

kotlin

Copy code

`val filteredList = list.filter { it.startsWith("A") }`

---

### 4. **Null Safety (ایمنی در برابر null)**

#### Java:

Java نیازمند مدیریت دستی null است:

java

Copy code

`List<String> list = new ArrayList<>(); list.add(null); if (list.get(0) != null) {     System.out.println(list.get(0)); }`

#### Kotlin:

Kotlin به صورت پیش‌فرض از **null safety** پشتیبانی می‌کند:

kotlin

Copy code

`val list: List<String?> = listOf(null, "A", "B") list.forEach { it?.let { println(it) } }`

---

### 5. **Syntax (خوانایی و مختصر بودن کد)**

#### Java:

java

Copy code

`Map<Integer, String> map = new HashMap<>(); map.put(1, "One"); map.put(2, "Two"); System.out.println(map.get(1));`

#### Kotlin:

kotlin

Copy code

`val map = mapOf(1 to "One", 2 to "Two") println(map[1])`

---

### 6. **Immutable vs Mutable**

#### Java:

در Java، مجموعه‌های **immutable** به صورت پیش‌فرض وجود ندارند و باید از کلاس‌های خاصی استفاده کرد (مثل `Collections.unmodifiableList`):

java

Copy code

`List<String> unmodifiableList = Collections.unmodifiableList(Arrays.asList("A", "B"));`

#### Kotlin:

در Kotlin، مجموعه‌ها به صورت پیش‌فرض **immutable** هستند:

kotlin

Copy code

`val list = listOf("A", "B")  // نمی‌توانید به آن آیتم اضافه کنید val mutableList = mutableListOf("A", "B")  // قابل تغییر است`

---

### 7. **Performance (عملکرد)**

- **Java** و **Kotlin** هر دو از **Collections Framework** یکسانی استفاده می‌کنند، بنابراین از نظر عملکرد تفاوتی ندارند.
- با این حال، مختصر بودن و کد کمتر در Kotlin می‌تواند منجر به خطای کمتر و توسعه سریع‌تر شود.

---

### نتیجه‌گیری:

- **Kotlin** به دلیل استفاده از توابع سطح بالا (مثل `filter`, `map`) و تمرکز روی خوانایی و سادگی، کار با مجموعه‌ها را بسیار راحت‌تر کرده است.
- اگر از **Java** به **Kotlin** مهاجرت می‌کنید، کار با مجموعه‌ها یکی از زمینه‌هایی است که بیشترین بهبود را حس می‌کنید.

4o