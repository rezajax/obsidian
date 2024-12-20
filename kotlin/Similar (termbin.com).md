


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


```kotlin
package com.example  
  
import io.ktor.network.selector.ActorSelectorManager  
import io.ktor.network.sockets.aSocket  
import io.ktor.server.application.*  
import io.ktor.server.engine.*  
import io.ktor.server.netty.*  
import kotlinx.coroutines.Dispatchers  
import kotlinx.coroutines.launch  
import java.net.InetSocketAddress  
  
fun main() {  
    embeddedServer(Netty, port = 9999, host = "0.0.0.0") {  
//        configureRoutingRez()  
    }.start(wait = true)  
}  
  
  
/*  
fun Application.launchTCPServer() {  
    launch(Dispatchers.IO) {        val serverSocket = aSocket(ActorSelectorManager(Dispatchers.IO)).tcp().bind(InetSocketAddress("0.0.0.0", 9999))        println("Listening for raw TCP connections on port 9999...")  
        while (true) {            val clientSocket = serverSocket.accept()            println("Client connected: ${clientSocket.remoteAddress}")  
            launch {                clientSocket.use { socket ->                    val input = socket.openReadChannel().bufferedReader()                    val output = socket.openWriteChannel(autoFlush = true).bufferedWriter()  
                    // Read data sent by the client                    val receivedData = input.readLine()                    println("Received: $receivedData")  
                    // Respond to the client                    val response = "Received: $receivedData\n"                    output.write(response)                    output.flush()                }            }        }    }}*/
```