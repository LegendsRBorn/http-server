# C HTTP Server 

A HTTP web server written in C using POSIX sockets. This helps us demonstrate core systems programming concepts including network socket programming, manual memory management, pointer-based string parsing, binary/text file I/O, bitwise configuration flags, and signal handling.

---

## Project Structure

```text
c-http-server/
├── Makefile                # Compiles all .c files into the final executable
├── server.conf             # Text file storing Port, Root Dir, and Flag settings
├── access.log              # Output file where server writes visitor logs
├── include/                # Header files (Structs, Macros, Function Prototypes)
│   ├── server.h            # Socket setup prototypes, global config structs
│   ├── http.h              # HTTP request/response structs, bitmask flags, unions
│   ├── file_ops.h          # Binary/Text file loader & MIME type prototypes
│   └── logger.h            # Logging macros and text file logging prototypes
├── src/                    # Source code files
│   ├── main.c              # Entry point: reads config, starts loop, handles signals
│   ├── server.c            # Socket bind/listen/accept logic
│   ├── http.c              # String/Pointer parsing of GET/POST requests
│   ├── file_ops.c          # Reads HTML/images using fread/fseek/ftell & malloc
│   └── logger.c            # Appends request logs to access.log using fprintf
└── www/                    # Static frontend files hosted by the server
    ├── index.html          # Main landing page
    ├── style.css           # Stylesheet
    └── logo.png            # Sample binary image asset
---

## Features

* **POSIX Socket Networking:** Full TCP socket lifecycle (`socket`, `bind`, `listen`, `accept`) capable of handling incoming client connections.
* **HTTP Request Parsing:** Custom string and pointer arithmetic parser for `GET` and `POST` requests, extracting methods, URIs, headers, and payloads using structured types, bitmask flags, and unions.
* **Static & Binary File Serving:** Dynamically reads and serves both text (`HTML`, `CSS`) and binary (`PNG`, `JPG`, etc.) assets from the `www/` directory using `fseek`, `ftell`, `fread`, and dynamic heap allocation (`malloc`/`free`).
* **MIME Type Resolution:** Automatically detects file extensions and attaches the appropriate `Content-Type` headers.
* **External Configuration:** Reads server parameters (Port, Root Directory, operational flags) at runtime via `server.conf` without requiring recompilation.
* **Access Logging:** Appends formatted visitor and request metadata directly to `access.log` using buffered file streams (`fprintf`).
* **Graceful Shutdown:** Intercepts OS signals (such as `SIGINT`) in the main event loop to cleanly close active file descriptors and free allocated memory before exiting.
