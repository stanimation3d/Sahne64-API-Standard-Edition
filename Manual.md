# Sahne64 API Standard Edition - User Manual

Sahne64 is a multi-language API designed to simulate nostalgic 64-bit based graphics and system functions on modern systems or to simplify low-level graphical operations. This manual is based on the analysis of the core files (sahne64.rs, sahne.h, main.cpp, etc.) developed for C, C++, Rust, and D.

1. Core Concepts and Getting Started
Sahne64 relies on a standard C interface (sahne.h) to maximize portability. Other languages (Rust, D) build wrappers or direct bindings over this C interface.
File Structure
* "sahne.h": Header file defining C/C++ protocols and API signatures.
* "sahne64.rs": Rust implementation and system integration logic.
* "main.*": Usage examples in various supported languages.

3. API Functions and Data Structures
Basic Data Types
The API generally utilizes the following standards:

* "s64_int": 64-bit integer.
* "s64_float": 64-bit floating-point number.
* "s64_color": RGBA format color values.
Core Functions

"sahne_init()"
Initializes the system and the graphics engine.
* Return Value: 0 on success, error code on failure.

"sahne_create_window(width, height, title)"
* Creates a window with specified dimensions and title.

"sahne_clear(color)"
* Clears the screen with the specified color. Typically called at the start of every frame.

"sahne_update()"
* Processes input events and refreshes the display.

5. Language-Specific Usage
C and C++ Usage
In C++ projects, you can perform direct function calls by including the sahne.h header.
```
#include "sahne.h"

int main() {
    if (sahne_init() == 0) {
        sahne_create_window(800, 600, "Sahne64 C++ Example");
        
        while (sahne_is_running()) {
            sahne_clear(S64_COLOR_BLACK);
            // Rendering logic goes here
            sahne_update();
        }
    }
    sahne_shutdown();
    return 0;
}
```

Rust Usage (sahne64.rs)
In Rust, the API is usually encapsulated within a struct to ensure memory safety and idiomatic usage.
```
use sahne64;

fn main() {
    let mut app = sahne64::Sahne::new();
    app.init(800, 600, "Sahne64 Rust");

    while app.is_running() {
        app.clear([0.1, 0.1, 0.1, 1.0]);
        // Rust-specific safe drawing commands
        app.update();
    }
}
```

D Language Usage (main.d)
The D language communicates directly with the C library using extern(C) blocks.
```
import sahne;

void main() {
    sahne_init();
    scope(exit) sahne_shutdown();

    sahne_create_window(1024, 768, "Sahne64 D Example");
    // ... loop and update ...
}
```

4. Graphics and Drawing Commands
The API provides several fundamental drawing capabilities:
1. Point/Pixel Drawing: "sahne_draw_pixel(x, y, color)"
2. Geometric Shapes: "draw_rect", "draw_circle", "draw_line".
3. Texture Management: Loading images and rendering them to the screen (sprite operations).

6. Debugging and Tips
* Memory Management: Always remember to call "sahne_shutdown()" if you are using C/C++ to prevent leaks.
* FPS Capping: "Use the sahne_set_target_fps(limit)" function to optimize CPU usage.
* Input Handling: Capture keyboard inputs using the "sahne_get_key(KEY_CODE)" function.

8. Compilation Notes
* C/C++: "gcc main.c -lsahne64"
* Rust: "cargo build" (Dependencies must be defined in "Cargo.toml").
* D: "dmd main.d sahne.lib"

This document was automatically generated based on the Sahne64 API Standard Edition source code.
