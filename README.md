<div align="center">

# 🦐 Shrimp-Editor
### The Editor That Lives in the Terminal's Subconscious

![Language](https://img.shields.io/badge/Language-C99-00599C?style=for-the-badge&logo=c&logoColor=white)
![Dependencies](https://img.shields.io/badge/Dependencies-Zero-ff0055?style=for-the-badge&logo=void-linux&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-a6da95?style=for-the-badge)

</div>

---

## ⚡ The Manifesto
**Shrimp** is not a wrapper. It is a lightweight, terminal-based text editor written from scratch in **C**.

We rejected heavy libraries like `ncurses`. Why? Because true systems wizards interact directly with the kernel via the `termios` struct and standard VT100 escape sequences. This project is a deep dive into systems programming, manual memory management, and the chaotic beauty of low-level terminal I/O.

> "Bloat is the enemy. Latency is death."

## 💎 Design Philosophy

| Core Tenet | Description |
| :--- | :--- |
| **Minimalism** | No config files. No plugins. Just code. |
| **Transparency** | Every byte sent to the terminal is intentional. |
| **Performance** | Dynamic buffers ensure efficient memory usage. |
| **Pure Posix** | Builds on any POSIX system with just `gcc`. |

## 🛠️ The Arsenal (Features)

- [x] **Raw Mode**: Canonical mode disabled. We process bytes, not lines.
- [ ] **Line Editing**: Surgical insertion and deletion.
- [ ] **Infinite Scroll**: Viewports that handle files larger than your screen.
- [ ] **Search**: Incremental search via linear scanning.
- [ ] **Syntax Highlighting**: ANSI-colored keywords for C/C++.

## 💾 Installation & Build

You need a C compiler and a desire to compile.

```bash
# Clone the repository
git clone https://github.com/Shrimanpro/shrimp-editor.git
cd shrimp-editor

# Compile the binary
make

# Execute
./shrimp filename.txt
```

## 🧠 Internals (Memory Dump)

### 0x01: Terminal Raw Mode
Standard terminals buffer input until `Enter`. We disable this.
Shrimp hijacks `termios` to disable `ECHO`, `ICANON`, and signal processing (`Ctrl-C`, `Ctrl-Z`). We control the flow now.

### 0x02: Double Buffered Rendering
Flickering is for amateurs. Shrimp utilizes a dynamic `abuf` (append buffer) strategy. We construct the entire screen in memory and blast it to `stdout` in a single `write()` syscall.

### 0x03: Data Structures
* **`erow`**: The atomic unit of a text line.
* **`editorConfig`**: The global state machine tracking cursor coordinates and window size.

## 🗺️ Roadmap
* **Phase 1:** Raw mode & Input handling 
* **Phase 2:** Viewport scrolling & File I/O (Current)
* **Phase 3:** Search & Syntax Highlighting
* **Phase 4:** Custom status bar

## 🤝 Contributing
This is a solo educational voyage, but if you find a segfault, open an issue.<div align="center">
*"It's small, but it bites."*
</div>

---

