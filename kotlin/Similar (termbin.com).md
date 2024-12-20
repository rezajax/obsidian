


```kotlin
package com.example  
  
import io.ktor.http.*  
import io.ktor.server.application.*  
import io.ktor.server.request.*  
import io.ktor.server.response.*  
import io.ktor.server.routing.*  
import java.io.File  
import java.util.UUID  
  
val linkMap = mutableMapOf<String, String>()  
  
fun Application.configureRouting() {  
    routing {  
        get("/") {  
            call.respondText("""  
                <html>                    <body>                        <form action="/" method="post">                            <input type="text" name="text" value="hi from browser" />                            <button type="submit">Send</button>                        </form>                    </body>                </html>            """.trimIndent(), contentType = io.ktor.http.ContentType.Text.Html)  
        }  
        post("/") {  
            val text = call.receiveText()  
            val uuid = UUID.randomUUID().toString()  
            val fileName = "received_text_$uuid.txt"  
            File(fileName).writeText(text)  
            val shortLink = uuid.take(8)  
            linkMap[shortLink] = fileName  
            call.respondText("Text received and saved. View it at <a href=\"http://localhost:9999/view/$shortLink\">http://localhost:9999/view/$shortLink</a>", contentType = ContentType.Text.Html)  
        }  
        get("/view/{shortLink}") {  
            val shortLink = call.parameters["shortLink"]  
            val fileName = linkMap[shortLink]  
            if (fileName != null) {  
                val fileContent = File(fileName).readText()  
                call.respondText(fileContent)  
            } else {  
                call.respondText("File not found", status = io.ktor.http.HttpStatusCode.NotFound)  
            }  
        }  
    }}
```


