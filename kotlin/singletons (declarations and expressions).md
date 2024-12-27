https://kotlinlang.org/docs/object-declarations.html#object-declarations-overview

object در کاتلین جیه؟

###### ChatGPT said:

ChatGPT

در زبان برنامه‌نویسی **کاتلین**، کلمه کلیدی `object` برای تعریف یک **شیء (Object)** استفاده می‌شود. `object` در کاتلین مفاهیم مختلفی دارد و در سه کاربرد اصلی مورد استفاده قرار می‌گیرد:

---

### 1. **Object Declaration (تعریف شیء)**

این نوع برای تعریف یک شیء singleton (یعنی شیء‌ای که فقط یک نمونه از آن وجود دارد) استفاده می‌شود.

kotlin

Copy code

`object MySingleton {     val name = "Singleton"     fun sayHello() = println("Hello from $name") }  fun main() {     MySingleton.sayHello() // خروجی: Hello from Singleton }`

- این شیء بدون نیاز به ساختن نمونه (instance) قابل استفاده است.
- معمولاً برای مدیریت حالت مشترک یا ایجاد یک **singleton pattern** استفاده می‌شود.

---

### 2. **Object Expression (شیء بی‌نام)**

با استفاده از این مفهوم، می‌توانید یک شیء **بی‌نام (Anonymous)** ایجاد کنید که یک نسخه سفارشی از یک کلاس یا اینترفیس باشد.

kotlin

Copy code

`fun main() {     val obj = object {         val x = 10         val y = 20         fun add() = x + y     }     println(obj.add()) // خروجی: 30 }`

یا برای **پیاده‌سازی یک اینترفیس:**

kotlin

Copy code

`interface ClickListener {     fun onClick() }  fun main() {     val listener = object : ClickListener {         override fun onClick() {             println("Button clicked!")         }     }     listener.onClick() // خروجی: Button clicked! }`

- در اینجا شیء بی‌نام به صورت مستقیم ایجاد می‌شود.

---

### 3. **Companion Object (شیء همراه)**

در یک کلاس، می‌توانید یک **شیء همراه (Companion Object)** تعریف کنید تا اعضای استاتیک (static-like) ایجاد کنید.

kotlin

Copy code

`class MyClass {     companion object {         val name = "Companion Object"         fun greet() = println("Hello from $name")     } }  fun main() {     MyClass.greet() // خروجی: Hello from Companion Object     println(MyClass.name) // خروجی: Companion Object }`

- `companion object` جایگزین اعضای استاتیک در جاوا است.
- می‌توانید یک **نام** برای `companion object` انتخاب کنید یا از نام پیش‌فرض آن استفاده کنید.

---

### خلاصه:

- **`object` declaration** برای ساخت singleton.
- **`object` expression** برای ایجاد شیء بی‌نام.
- **`companion object`** برای دسترسی به اعضای مشابه static در کلاس‌ها.

اگر مورد خاصی مد نظر دارید، می‌توانید مثال دقیق‌تری بدهید تا توضیح بیشتری ارائه دهم. 🙂

4o

##### You said:

object Tasks : Table("tasks") { val id = integer("id").autoIncrement() val title = varchar("name", MAX_VARCHAR_LENGTH) val description = varchar("description", MAX_VARCHAR_LENGTH) val isCompleted = bool("completed").default(false) } این شامل کدوم یک از این سه تاس؟

###### ChatGPT said:

ChatGPT

کدی که ارائه دادید متعلق به کتابخانه **Exposed** در کاتلین است (یک ORM برای ارتباط با دیتابیس)، و در اینجا `object Tasks` یک **Object Declaration** است. این شیء به صورت یک **singleton** تعریف شده است و نمایانگر جدولی در دیتابیس با نام `tasks` است.

---

### دلیل اینکه این یک Object Declaration است:

1. با کلمه کلیدی `object` تعریف شده است.
2. به عنوان یک **singleton** عمل می‌کند، چون فقط یک نمونه از این شیء وجود دارد.
3. اعضای آن (مثل `id`, `title`, `description` و غیره) ویژگی‌هایی هستند که ساختار جدول دیتابیس را تعریف می‌کنند.
4. از کلاس `Table` ارث‌بری کرده است که بخشی از کتابخانه **Exposed** است.

---

### توضیح:

این `object` نماینده جدول `tasks` در دیتابیس شما است. وقتی از کتابخانه Exposed استفاده می‌کنید، معمولاً جداول را به این صورت تعریف می‌کنید. برای مثال، شما می‌توانید عملیات‌های مرتبط با این جدول (مثل `insert`, `select`, `update`) را از طریق همین `object` مدیریت کنید.

---

### نمونه استفاده:

برای استفاده از این جدول، می‌توانید به شکل زیر عمل کنید:

kotlin

Copy code

`transaction {     // اضافه کردن یک ردیف جدید به جدول     Tasks.insert {         it[title] = "Learn Kotlin"         it[description] = "Study Kotlin programming language and its features"         it[isCompleted] = false     }          // دریافت همه ردیف‌ها     Tasks.selectAll().forEach {         println("${it[Tasks.id]}: ${it[Tasks.title]} - ${it[Tasks.isCompleted]}")     } }`

---

### جمع‌بندی:

این یک **Object Declaration** است که معمولاً در کاتلین برای ایجاد singletonها استفاده می‌شود. در اینجا از آن برای تعریف یک جدول دیتابیس به کمک کتابخانه Exposed بهره گرفته شده است.

4o