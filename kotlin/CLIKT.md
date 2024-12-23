
```kotlin
plugins {
    kotlin("jvm") version "1.9.10" // Adjust the version to match your Kotlin version
    id("application")
}

repositories {
    mavenCentral()
}

dependencies {
	implementation("com.github.ajalt.clikt:clikt:5.0.1")
	
	// optional support for rendering markdown in help messages  
	implementation("com.github.ajalt.clikt:clikt-markdown:5.0.1")
}

application {
    mainClass.set("com.example.MainKt") // Set this to your main class path
}

tasks.jar {
    manifest {
        attributes["Main-Class"] = "com.example.MainKt" // Adjust to match your main class
    }
    from(sourceSets.main.get().output)

    // Include runtime dependencies
    dependsOn(configurations.runtimeClasspath)
    from({
        configurations.runtimeClasspath.get().filter { it.name.endsWith("jar") }.map { zipTree(it) }
    })
}
```



export with shadow jar
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

export with custom tasks
```kotlin
tasks.register<Jar>("fatJarCustom") {  
    group = "build"  
    description = "Assembles a fat JAR that includes all dependencies." 
     
	// rez: add suffix on file
    archiveClassifier.set("fat")  
  
    duplicatesStrategy = DuplicatesStrategy.EXCLUDE  
  
    manifest {  
        attributes(  
            "Main-Class" to "MainKt" // مسیر کامل کلاس اصلی شما  
        )  
    }  
  
    from(sourceSets.main.get().output)  
  
    // اضافه کردن دپندنسی‌ها  
    dependsOn(configurations.runtimeClasspath)  
    from({  
        configurations.runtimeClasspath.get().filter { it.name.endsWith("jar") }.map { zipTree(it) }  
    })  
}
```

```kotlin
package com.example

import com.github.ajalt.clikt.core.CliktCommand

class MyApp : CliktCommand() {
    override fun run() {
        println("Hello, Clikt!")
    }
}

fun main(args: Array<String>) = MyApp().main(args)
```




if we don't want use "CLIKT"
https://kotlinlang.org/docs/jvm-get-started.html#run-the-application 
```kotlin
fun main() {
    println("What's your name?")
    val name = readln()
    println("Hello, $name!")

    // ...
}
```