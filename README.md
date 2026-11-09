# 🌐 C HTTP Web Server: Building the Web from Scratch

Written in C, this project demonstrates an understanding of core systems programming, POSIX network sockets, memory management, and file I/O.

## Features

* **Dynamic Configuration:** Reads server settings (port, root directory, flags) on startup from `server.conf`.
* **Static File Hosting:** Successfully serves HTML, CSS, and JS to render modern web pages.
* **Binary File Streaming:** Safely calculates and transmits raw binary files (like PNG/JPG images) over TCP sockets without data corruption.
* **Real-time Access Logging:** Automatically records incoming requests, timestamps, and HTTP response codes to an `access.log` text file.
* **Memory Safety:** Strictly manages heap allocations (`malloc`/`calloc`) for incoming request buffers and ensures graceful memory releases (`free`) to prevent leaks.

## File Architecture
what each module is responsible for:

### Source Files (`src/`)
* **`main.c` (The Orchestrator):** The entry point of the server. It reads the `server.conf` file using text I/O (`fgets`), initializes the server state, and manages the main infinite loop that keeps the server alive.
* **`server.c` (The Networking Core):** Wraps the complex POSIX socket API. It handles creating the socket, binding it to a port, listening for traffic, and accepting incoming client connections.
* **`http.c` (The Protocol Engine):** The brain of request handling. It uses advanced pointer arithmetic to parse raw HTTP request strings (extracting GET/POST methods and URIs) without relying on heavy string-copying, ensuring high performance.
* **`file_ops.c` (The File System Bridge):** Manages all disk interactions. Matches requested file extensions to MIME types, uses binary file I/O (`fseek`, `ftell`, `fread`) to determine exact file sizes, and loads files into dynamically allocated memory blocks for transmission.
* **`logger.c` (The Observability Module):** Handles writing server events and access logs to `access.log` using standard `fprintf`. 

### Header Files (`include/`)
* **`*.h` files:** Act as the architectural blueprints. They contain our `#define` macros (buffer sizes, status codes), custom `structs` (like `HttpRequest` and `ServerConfig`), `unions`, and all function prototypes to ensure strict type-checking across the codebase.

## 📚 Syllabus Concepts Mastered

* **Pointers vs Strings:** Efficient memory navigation without relying on basic arrays.
* **Dynamic Memory Management:** Robust use of `malloc`, `calloc`, and `free`.
* **Text & Binary File Operations:** Mastery of both character-stream and raw byte-stream file handling.
* **Abstract Data Types:** Heavy utilization of `structs` to manage complex network states and `unions` for memory-efficient data representation.
* **Bitwise Operations:** Used for setting and reading application configuration flags.

## run 

### 1. Compile the server
Run the provided Makefile from the root directory to compile all source files into a single executable:
```bash
make
```

### 2. Configure the server
Check `server.conf` to ensure your desired port is set (default is usually `8080`).

### 3. Start the server
Execute the compiled binary:
```bash
./http_server
```

### 4. Test it out
Open your favorite web browser and navigate to:
`http://localhost:8080/index.html`

To view the server logs, open `access.log` in your terminal:
```bash
cat access.log
```

## 👥 The Engineers

IDEAS:**[ARYAN SARDA]** & **[ANANYA SINGH]**