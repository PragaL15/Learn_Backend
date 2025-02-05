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

5. 

`