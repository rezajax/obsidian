
```kotlin
import java.net.ServerSocket
import java.net.Socket
import java.io.InputStream
import java.io.OutputStream


fun main() {

    val ali = 0xFF
    println(ali)
    val serverSocket = ServerSocket(1122) // گوش دادن بر روی پورت 1080 برای SOCKS5
    println("SOCKS5 Server is running on port 1080...")

    while (true) {
        val clientSocket = serverSocket.accept() // قبول کردن اتصال از کلاینت
        println("Accepted a connection from ${clientSocket.inetAddress}")
        handleClient(clientSocket)
    }
    val version = 0x05

}

fun handleClient(socket: Socket) {
    val input: InputStream = socket.getInputStream()
    val output: OutputStream = socket.getOutputStream()

    // مرحله 1: Handshake - خواندن درخواست handshake از کلاینت
    val version = input.read()
    println("Received version: $version")

    if (version == 0x05) {
        // 0o
        // 0b110
        //
        println("SOCKS5 version supported")
        output.write(0x05) // جواب دادن با SOCKS5 version

        // مرحله 2: Authentication - بررسی نوع احراز هویت
        val numAuthMethods = input.read()
        println("Number of authentication methods: $numAuthMethods")

        val authMethods = ByteArray(numAuthMethods)
        input.read(authMethods)
        println("Authentication methods: ${authMethods.joinToString(", ")}")

        // فرض بر اینکه هیچ احراز هویتی مورد نیاز نیست
        output.write(0x05) // هیچ احراز هویتی نیاز نیست
        println("No authentication required")

        // مرحله 3: درخواست اتصال
        val command = input.read()
        println("Received command: $command")

        if (command == 0x01) { // CONNECT command
            println("CONNECT command received")

            // نوع آدرس
            val addressType = input.read()
            println("Address type: $addressType")

            val address = when (addressType) {
                0x01 -> { // IPv4 address
                    val ip = ByteArray(4)
                    input.read(ip)
                    ip.joinToString(".") { it.toString() }
                }
                else -> throw Exception("Unsupported address type")
            }
            val port = (input.read() shl 8) + input.read()
            println("Connecting to $address:$port")

            // مرحله 4: اتصال به مقصد
            try {
                val destinationSocket = Socket(address, port)
                println("Successfully connected to $address:$port")

                output.write(0x05) // تایید موفقیت آمیز
                output.write(0x00) // هیچ خطایی نیست
                println("Connection successful")

                // اکنون داده‌ها می‌توانند انتقال یابند (مرحله انتقال داده‌ها)
                // این بخش می‌تواند شامل انتقال داده‌ها از کلاینت به سرور مقصد و برعکس باشد
            } catch (e: Exception) {
                println("Failed to connect to $address:$port - ${e.message}")
                output.write(0x05) // خطای اتصال
                output.write(0x01) // خطای اتصال عمومی
            }
        }
    }

    socket.close()
    println("Closed connection with ${socket.inetAddress}")
}
```


working:
```kotlin

import java.io.*
import java.net.ServerSocket
import java.net.Socket


fun main() {
//    val input: InputStream = Socket
    val serverSocket = ServerSocket(1122)
    println("SOCKS5 Server is running on port ${serverSocket.localPort} ...")


    while (true) {

        val clientSocket = serverSocket.accept()
        println("Accepted a connection from ${clientSocket.toString()}")

        handleClient(clientSocket)
    }


}

fun handleClient(socket: Socket) {
    socket.use { // Ensures the socket is closed after handling
        val input = socket.getInputStream()
        val output = socket.getOutputStream()

        println("Client connected: ${socket.remoteSocketAddress}")

        // Read and print client data
        try {
            val reader = BufferedReader(InputStreamReader(input))
            val writer = PrintWriter(OutputStreamWriter(output), true)

            // Send initial server response (if required)
            writer.println("Hello! You are connected to the SOCKS5 Server.")

            var line: String?
            while (reader.readLine().also { line = it } != null) {
                println("Received from client: $line")
                // Echo the data back to the client (or implement SOCKS5 protocol logic here)
                writer.println("Server received: $line")
            }
        } catch (e: IOException) {
            println("Error handling client: ${e.message}")
        }

        println("Client disconnected: ${socket.remoteSocketAddress}")
    }
}



```

test: 
```bash
nc localhost 1122
```

add this snippet code for get local IP address.
```kotlin
fun getLocalIpAddress(): String? {  
    try {  
        val networkInterfaces = NetworkInterface.getNetworkInterfaces()  
        for (networkInterface in networkInterfaces) {  
            if (!networkInterface.isUp || networkInterface.isLoopback) continue  
  
            val addresses = networkInterface.inetAddresses  
            for (address in addresses) {  
                if (!address.isLoopbackAddress && address is InetAddress && address.hostAddress.indexOf(':') == -1) {  
                    return address.hostAddress // Return IPv4 address  
                }  
            }  
        }  
    } catch (e: Exception) {  
        println("Error retrieving local IP address: ${e.message}")  
    }  
    return null  
}
```


This snippet is show a hex stream!
```kotlin
fun handleClient(socket: Socket) {
    socket.use { // Ensures the socket is closed after handling
        val input = socket.getInputStream()
        val output = socket.getOutputStream()

        println("Client connected: ${socket.remoteSocketAddress}")

        // Read and print client data
        try {
            val buffer = ByteArray(1024) // Buffer for reading data
            var bytesRead: Int

            while (input.read(buffer).also { bytesRead = it } != -1) {
                // Convert the bytes to hexadecimal representation
                val hexData = buffer.copyOf(bytesRead).joinToString(" ") { "%02x".format(it) }
                println("Received (${bytesRead} bytes): $hexData")
            }

            // Optional: Send a response to the client
            val writer = PrintWriter(OutputStreamWriter(output), true)
            writer.println("Server received your data.")
        } catch (e: IOException) {
            println("Error handling client: ${e.message}")
        }

        println("Client disconnected: ${socket.remoteSocketAddress}")
    }
}

```