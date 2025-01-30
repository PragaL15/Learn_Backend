### Log in golang
---

### **1️⃣ Basic Logging (Print to Console)**
```go
package main

import (
	"log"
)

func main() {
	log.Println("Application started") // Info log
	log.Println("Processing request...")
	log.Println("Task completed successfully")
}
```
🔹 **Use Case:** General application logging.

---

### **2️⃣ Logging Errors**
```go
package main

import (
	"log"
	"os"
)

func main() {
	_, err := os.Open("non_existent_file.txt")
	if err != nil {
		log.Println("Error:", err) // Logs error without stopping execution
	}
}
```
🔹 **Use Case:** Capturing non-critical errors.

---

### **3️⃣ Fatal Logging (Stops Execution)**
```go
package main

import (
	"log"
)

func main() {
	log.Fatal("Critical error: Database connection failed!") 
	// Stops execution after logging
}
```
🔹 **Use Case:** When encountering unrecoverable errors.

---

### **4️⃣ Panic Logging (Logs & Panics)**
```go
package main

import (
	"log"
)

func main() {
	log.Panic("Unexpected error occurred!") // Logs and causes a panic
}
```
🔹 **Use Case:** Debugging unexpected failures.

---

### **5️⃣ Logging to a File**
```go
package main

import (
	"log"
	"os"
)

func main() {
	file, err := os.OpenFile("app.log", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
	if err != nil {
		log.Fatal(err)
	}
	defer file.Close()

	log.SetOutput(file) // Redirect logs to file

	log.Println("Application started")
	log.Println("User logged in")
}
```
🔹 **Use Case:** Storing logs for future reference.

---

### **6️⃣ Custom Log Format**
```go
package main

import (
	"log"
)

func main() {
	log.SetFlags(log.Ldate | log.Ltime | log.Lshortfile) // Adds date, time, and file location
	log.Println("Application started")
}
```
🔹 **Use Case:** Adding more context to logs.

---

### **Conclusion**
The **built-in `log` package** is simple and efficient for general logging in Golang. For more complex needs (structured logging, log rotation), external libraries like `logrus` or `zap` can be used.  
