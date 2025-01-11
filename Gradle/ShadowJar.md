## 1
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

# 2

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