1. `os/signal` - Is used mostly when an appliction needs a `graceful shutdown`, which means **cleaning up the connection before shutting down**.
2. `SIGINT` - sent when we press Ctrl+C.
    `SIGTERM` - Standard termination signal from external.
    `SIGUP` - When terminal session is closed
    