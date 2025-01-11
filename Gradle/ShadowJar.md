## 1 new
https://plugins.gradle.org/plugin/com.gradleup.shadow

```kotlin
plugins {  
    id("com.gradleup.shadow") version "9.0.0-beta4"  
//    kotlin("jvm") version "2.0.21"  
    kotlin("jvm")  
}

tasks {  
    shadowJar {  
        // Specify the main class to run  
        manifest {  
            attributes["Main-Class"] = "ir.rezajax.MainKt" // Replace with your main class path  
        }  
        archiveBaseName.set("my-shadow-jar") // Name of the JAR file  
        archiveVersion.set("1.0.0") // Set the version if necessary  
        mergeServiceFiles() // Optional: Merges service files from dependencies  
    }
}

```

# 2 old

https://plugins.gradle.org/plugin/com.github.johnrengelman.shadow
![[Pasted image 20250112003122.png]]
```kotlin 
// put in plugins
id("com.github.johnrengelman.shadow") version "8.1.1"

tasks.named<Jar>("shadowJar") {
    group = "build"
    description = "build with shadowJAR"

    archiveClassifier.set("shadow")

    manifest {
        attributes("Main-Class" to "MainKt") // نام کلاس اصلی
    }
}
```

دلیل تفاوت در پیاده‌سازی این دو نمونه استفاده از **دو پلاگین مختلف** برای ساخت فایل Shadow JAR است. هر پلاگین روش خاص خود را برای تعریف وظایف و پیکربندی‌ها دارد.

### توضیح دو پلاگین:

1. **پلاگین `com.gradleup.shadow`**:
    
    - این پلاگین نسخه‌ای غیررسمی از پلاگین Shadow است که توسط GradleUp توسعه یافته است.
    - سینتکس و تنظیمات آن کمی مدرن‌تر و مبتنی بر DSLهای جدید Gradle است.
    - در این پلاگین، وظایف ShadowJar به صورت مستقیم در قالب `tasks` تعریف می‌شود.
2. **پلاگین `com.github.johnrengelman.shadow`**:
    
    - این پلاگین نسخه رسمی Shadow است که توسط جامعه Kotlin و Gradle به‌طور گسترده استفاده می‌شود.
    - این پلاگین به‌صورت استاندارد پیکربندی وظایف را با استفاده از متد `tasks.named<Jar>` ارائه می‌دهد.
    - همچنین نام پلاگین اشاره به نسخه پایدار و رسمی آن دارد.

---

### تفاوت‌ها در پیاده‌سازی:

#### 1. **تعریف `tasks`**:

- در پلاگین اول (`com.gradleup.shadow`): وظیفه `shadowJar` مستقیماً در بخش `tasks` تعریف می‌شود و به روشی ساده‌تر قابل پیکربندی است.
- در پلاگین دوم (`com.github.johnrengelman.shadow`): از متد `tasks.named<Jar>("shadowJar")` استفاده می‌شود که به نوع وظیفه (Task Type) اشاره دارد.

#### 2. **ساختار پیکربندی**:

- پلاگین اول از متد `manifest` به‌صورت مستقیم در داخل پیکربندی `shadowJar` استفاده می‌کند.
- پلاگین دوم از متد `manifest` به همراه یک آرایه `attributes` استفاده می‌کند.

#### 3. **امکانات اضافی**:

- پلاگین اول متدی مانند `mergeServiceFiles()` ارائه می‌دهد که فایل‌های سرویس‌ها را از وابستگی‌ها ادغام می‌کند.
- پلاگین دوم چنین متدی را مستقیماً در تنظیمات اولیه ارائه نمی‌دهد و ممکن است نیاز به تعریف دستی باشد.

---

### نکات مهم:

- اگر از نسخه رسمی و پایدار می‌خواهید استفاده کنید، بهتر است پلاگین `com.github.johnrengelman.shadow` را ترجیح دهید.
- اگر پلاگین مدرن‌تر با سینتکس خلاصه‌تر و امکانات پیشرفته‌تر را می‌خواهید، می‌توانید از `com.gradleup.shadow` استفاده کنید.

هر کدام را بر اساس نیاز پروژه و وابستگی‌هایتان انتخاب کنید.