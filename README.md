# Shrimp

![Language](https://img.shields.io/badge/language-C99-00599C?style=flat-square&logo=c)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![Dependencies](https://img.shields.io/badge/dependencies-none-red?style=flat-square)

**Shrimp** is a lightweight, terminal-based text editor written from scratch in C. 

It avoids heavy libraries like `ncurses` in favor of interacting directly with the kernel via the `termios` struct and standard VT100 escape sequences. This project serves as a deep dive into systems programming, memory management, and low-level terminal I/O.

##  Design Philosophy

* **Minimalism:** No bloat. No configuration files (yet).
* **Transparency:** Understand every byte sent to the terminal.
* **Performance:** Efficient memory usage via dynamic buffers.
* **Dependency-Free:** Builds on any POSIX-compliant system with just a C compiler.

##  Features

* [ ] **Raw Mode:** Custom `termios` handling to disable canonical mode, echo, and signals.
* [ ] **Line Editing:** Insert, delete, and append characters.
* [ ] **Scrollable Viewport:** Handle files larger than the screen.
* [ ] **Search:** Incremental search functionality.
* [ ] **Syntax Highlighting:** Basic support for C/C++ keywords.

##  Installation & Build

Shrimp requires a C compiler (GCC or Clang) and `make`.

```bash
# Clone the repository
git clone [https://github.com/Shrimanpro/shrimp.git](https://github.com/Shrimanpro/shrimp.git)
cd shrimp-editor

# Build the executable
make

# Run the editor
./shrimp filename.txt
```

##  Internals (For the curious)

### 1. Terminal Raw Mode
By default, terminals buffer input until `Enter` is pressed (Canonical mode). Shrimp disables this to process input byte-by-byte. It also disables `Ctrl-C`, `Ctrl-Z`, and output processing (like `\n` translation) to take full control.

### 2. Screen Rendering
Shrimp uses a **Double Buffering** strategy (via a dynamic `abuf` string) to write the entire screen refresh to the terminal in a single `write()` call. This prevents the "flickering" effect common in naive terminal apps.

### 3. Data Structures
* **`erow` (Editor Row):** Represents a single line of text.
* **`editorConfig`:** A global struct maintaining cursor state, screen dimensions, and terminal flags.

##  Roadmap

* **Phase 1:** Raw mode & Input handling (Current)
* **Phase 2:** Viewport scrolling & File I/O
* **Phase 3:** Search & Syntax Highlighting
* **Phase 4:** Custom status bar

##  Contributing

This is a solo educational project, but feel free to open issues if you find bugs on specific terminal emulators!

---

*"It's small, but it's mighty."*
