
```kotlin

fun listFilesInResourceDir(dirPath: String): List<String> {  
    val classLoader = Thread.currentThread().contextClassLoader  
    val resource = classLoader.getResource(dirPath)  
    val log: Logger = LoggerFactory.getLogger("ClassRez") // Replace with your class name  
  
    log.debug("Resource URI: $resource")  
  
    return if (resource != null) {  
        val uri = URI(resource.toString())  
  
        // If the resource is in a JAR, the scheme will be "jar"  
        if (uri.scheme == "jar") {  
            try {  
                val fileSystem = FileSystems.newFileSystem(uri, emptyMap<String, Any>())  
                val jarPath = fileSystem.getPath(dirPath)  
                Files.walk(jarPath, 1)  
                    .filter { Files.isRegularFile(it) }  
                    .map { it.fileName.toString() }  
                    .toList()  
            } catch (e: Exception) {  
                log.error("Error accessing JAR resources", e)  
                emptyList()  
            }  
        } else {  
            // If the resource is a regular directory (not in JAR), list the files normally  
            val path = Paths.get(uri)  
            log.debug("Resolved path: $path")  
            val file = File(path.toUri())  
            file.listFiles()?.map { it.name } ?: emptyList()  
        }  
    } else {  
        log.error("Resource not found: $dirPath")  
        emptyList()  
    }  
}

routing {  
    get("/html-thymeleaf") {  
        val files = listFilesInResourceDir("templates/thymeleaf")  
        call.respond(ThymeleafContent("index.html",  
            mapOf (  
                "user" to ThymeleafUser(1, "user1"),  
                "files" to files,  
            )))  
    }

```