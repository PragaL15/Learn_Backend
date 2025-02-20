### Goroutine

1. What is a channel in goroutine?

A `channel` in Go is a built-in data structure that allows `safe communication` between goroutines. It provides a way for goroutines to `send and receive data synchronously`, preventing race conditions and ensuring thread-safe concurrency.
 - Creating a channel that will send , recive int datatype
   - `ch := make(chan int) // Creates a channel for int values`

2. Without goroutines what are the effects we face?
  - Without goroutines, Go executes one task at a time, meaning a slow task (e.g., API call, database query) will block the entire program. With goroutine we could run the tasks simultaneously.

3. How the goroutine is been effectivly used?
  - Multiple tasks run on different CPU cores, maximizing performance and Ideal for CPU-intensive tasks.Go web server handles each request synchronously without goroutines, it can only process one request at a time, making it slow for high traffic.

4. How a Go Server Works?
- Client sends an HTTP request (e.g., browser, Postman, mobile app).
- Go server receives the request and processes it.
- Server executes logic (e.g., fetch data, process form, interact with a database).
- Server sends an HTTP response back to the client.

5. Golang uses the channels and mutex for synchronization.
 - Synchronisation means that ensures if the tasks are in correct order and prevent the conflict when multiple tasks run at same time.

---
**Note:** shared resources are any global variable, file or data struture that are accessed by multiple goroutines simultaneously. 
- Without proper synchronization concurrent access to a shared resource can lead to race conditions , data corruption etc.
--- 

6. What is mutex in golang? (Mutual Exclusion Lock)
 - It prevents the multiple goroutines from accessing a shared resouces simultaneously.
 - ```golang
  mu.Lock() //ensures only one Goroutine modifies counter at a time.
  mu.Unlock() //releases the lock for others.
  ```
 - This way we could lock bfr modifying shared variable and unlock aftr modification.

7. Real-time example for mutex?
  - Multiple users making payments at the same time may   cause incorrect balance updates due to race conditions.
  - Solution: A mutex ensures only one transaction updates an account balance at a time.

  will be used while taking the logs from appliation incase of debugging.

8. 