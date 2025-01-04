### Problem Description

The error encountered is:

```
java.lang.RuntimeException: Unable to start activity ComponentInfo{ir.rezajax.newproxyserver/ir.rezajax.newproxyserver.MainActivity}: android.os.NetworkOnMainThreadException
```

This indicates that a **network operation** (such as `ServerSocket.accept`) was performed on the **Main Thread**, which is not allowed on Android due to potential UI freezing and poor user experience.

### Cause of the Issue

On Android, long-running or blocking operations (e.g., networking, heavy file I/O, or database operations) cannot be executed on the **Main Thread**. Android enforces this through `**StrictMode**`, which throws a `NetworkOnMainThreadException` when such code is run on the main thread.

### Solution

You must move network operations, like `ServerSocket.accept()`, to a **separate thread** or a **background task**. Below are some ways to handle this:

---

#### Fix Using a `Thread`

Move the network operation to a new thread:

```
Thread {
    try {
        val serverSocket = ServerSocket(1122)
        while (true) {
            val socket = serverSocket.accept()
            // Process incoming data
        }
    } catch (e: Exception) {
        e.printStackTrace()
    }
}.start()
```

---

#### Fix Using Kotlin Coroutines

If you're using Kotlin Coroutines:

```
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.GlobalScope
import kotlinx.coroutines.launch
import kotlinx.coroutines.withContext

GlobalScope.launch(Dispatchers.IO) {
    try {
        val serverSocket = ServerSocket(1122)
        while (true) {
            val socket = serverSocket.accept()
            // Process incoming data
        }
    } catch (e: Exception) {
        e.printStackTrace()
    }
}
```

---

### Key Points

- Use `**Dispatchers.IO**` for I/O-bound operations like networking.
    
- **Avoid using** `**GlobalScope**` **indiscriminately**. Instead, use lifecycle-aware coroutines if your app structure allows it (e.g., with `ViewModel` or `CoroutineScope`).
    

---

### Additional Debugging

If the problem persists, carefully inspect the line of code where the issue originates, specifically `MainActivity.kt` line 50 as mentioned in the logs. The offending code must be offloaded to a background thread or coroutine.

### References

- [Android Documentation on StrictMode](https://developer.android.com/reference/android/os/StrictMode)
    
- Kotlin Coroutines Guide