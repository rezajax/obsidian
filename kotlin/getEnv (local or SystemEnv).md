
get System Env

```kotlin
val apiKey = System.getenv("TMDB_API") ?: throw IllegalStateException("API Key not set")  
println("from directFromJava: $apiKey")
```

 ```kotlin
//on main() fun
val apiKey2 = Config.TMDB_API  
println("TMDB API Key: $apiKey2")


object Config {  
    val TMDB_API: String = System.getenv("TMDB_API") ?: error("TMDB_API environment variable not set")  
}
```


getFrom local.properties

> [!NOTE] on Andorid
>  you can use in gradle

```kotlin
// Get From local.properties  
fun getApiKey(): String {  
    val props = Properties()  
    val inputStream = FileInputStream("local.properties")  
    props.load(inputStream)  
    return props.getProperty("TMDB_API") ?: throw IllegalStateException("API Key not found")  
}
```