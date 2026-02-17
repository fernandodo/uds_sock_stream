# CMake and Compiler Warnings Q&A

## 1. Executable Names in CMake
**Q: Is the name in `add_executable` the final binary file name?**  
**A:** Yes. `add_executable(server ...)` produces a binary named `server` (or `server.exe` on Windows). You run it as `./server`.

## 2. Include Directories: Target-based vs. Global
**Q: Why use `target_include_directories` instead of `include_directories`?**  
**A:** `target_include_directories` is "Modern CMake." It provides:
- **Encapsulation**: Only the specified target sees the headers.
- **Visibility Control**: Use `PRIVATE`, `PUBLIC`, or `INTERFACE` to control how headers propagate to other targets that link to this one.
- **Cleanliness**: Avoids "include pollution" where every target sees every header in the project.

**Q: If both targets use the `common` folder, why not use the global `include_directories`?**  
**A:** While it works for small projects, `target_include_directories` makes dependencies explicit. It ensures each target's "recipe" is self-contained and teaches good habits for larger, professional codebases.

## 3. Compiler Warnings (-Wall, -Wextra, -Wpedantic)
**Q: What are these three warnings for?**  
**A:** They act as a strict proofreader to catch bugs that aren't technically syntax errors:
- **`-Wall`**: Catches common bugs like uninitialized variables and missing return statements.
- **`-Wextra`**: Catches more subtle issues like comparing signed/unsigned integers or unused function parameters.
- **`-Wpedantic`**: Ensures the code strictly follows ISO C++ standards, making it more portable and avoiding compiler-specific "hacks."
