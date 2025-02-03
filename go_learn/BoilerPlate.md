#### Boilerplate Structure 
```
/project-root
│── /cmd             → Entry point (main.go)
│── /config          → Configuration files (env, DB config)
│── /internal
│   │── /handlers    → API handlers (controllers)
│   │── /services    → Business logic layer
│   │── /repository  → Database queries (SQL, GORM)
│   │── /models      → Structs and DTOs
│   │── /middlewares → Auth, logging, rate limiting
│── /pkg             → Reusable utilities (JWT, logging, etc.)
│── go.mod
│── go.sum
```

