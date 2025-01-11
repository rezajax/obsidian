include
```kotlin
include("moduleName")
```




If have this problem:

> The Kotlin Gradle plugin was loaded multiple times in different subprojects, which is not supported and may break the build. This might happen in subprojects that apply the Kotlin plugins with the Gradle 'plugins { ... }' DSL if they specify explicit versions, even if the versions are equal. Please add the Kotlin plugin to the common parent project or the root project, then remove the versions in the subprojects. If the parent project does not need the plugin, add 'apply false' to the plugin line.

```kotlin
plugins {  
    kotlin("jvm") version "2.0.21" apply false 
}
```

> [!NOTE] نکته
> `apply false` به این معناست که پلاگین فقط تعریف می‌شود اما به پروژه والد اعمال نمی‌شود. زیرپروژه‌ها از این تعریف استفاده می‌کنند.