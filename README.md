# C++ URL Shortener

A lightweight, high-performance URL shortener built with C++ and the [Crow](https://crowcpp.org/) web framework. This project features a clean, dark-themed web interface for users to shorten long URLs and automatically redirects visitors to the original destination using HTTP 301 status codes.

## Features

*   **Modern Web UI:** Includes a responsive HTML/CSS/JS frontend embedded directly in the binary.
*   **Persistent Storage:** Automatically saves and loads your URL mappings from `url_mapping.dat` so you don't lose links after restarting.
*   **HTTP Redirection:** Uses standard HTTP 301 (Moved Permanently) headers for fast, efficient link forwarding.
*   **Collision Handling:** Automatically handles potential ID clashes by appending a salt to the hash.

## Prerequisites

To compile this project, you will need:
1.  **G++ Compiler** (MinGW-w64 recommended for Windows).
2.  **Crow Framework:** Download `crow_all.h` from [Crow GitHub](https://github.com/CrowCpp/Crow/releases).
3.  **Asio:** Download the standalone `asio` library from [Asio sourceforge](https://sourceforge.net/projects/asio/files/asio/).

## Setup Instructions

1.  **Clone/Copy the project:** Ensure `url_shortner.cpp` is in your project folder.
2.  **Organize Dependencies:**
    *   Place `crow_all.h` in your project root.
    *   Place the `include` folder from Asio in your project root.
3.  **Compile:**
    Open your terminal in the project folder and run:
    ```bash
    g++ url_shortner.cpp -o shortener.exe -I include -lws2_32 -lmswsock
    ```
4.  **Run:**
    ```bash
    ./shortener.exe
    ```
5.  **Access:**
    Open your browser and navigate to `http://localhost:8080`.

## How It Works

*   **Shortening:** The server receives a URL, generates a 6-character hash using `time(0)`, and saves it to a local file.
*   **Redirecting:** When a user visits `/r/<short_id>`, the server looks up the ID in the `unordered_map` and issues a 301 redirect.
*   **Storage:** The program uses a simple file-based database (`url_mapping.dat`). It reads this file on startup and appends new entries in real-time.

## License
This project is open-source and available for educational use.