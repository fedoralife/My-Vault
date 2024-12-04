Sure! Below is a brief document on some of the most commonly used modules from the Rust standard library. This will help you get familiar with key parts of Rust's core functionality and understand how they work.

### 1. **`std::io`** - Input/Output
The `std::io` module provides the ability to handle input and output operations in Rust. You can read from and write to files, the terminal, or other streams.

- **Commonly Used Functions and Types:**
  - **`stdin()`**: Reads user input from standard input (keyboard).
  - **`stdout()`**: Used to write output to standard output (console).
  - **`read_line()`**: Reads a line of input from `stdin`.
  - **`write()` and `flush()`**: Writes to the output and ensures the buffer is flushed (useful for immediate display).

```rust
use std::io::{self, Write};

let mut input = String::new();
print!("Enter something: ");
io::stdout().flush().unwrap(); // Ensure the prompt is printed
io::stdin().read_line(&mut input).unwrap();
println!("You entered: {}", input.trim());
```

### 2. **`std::fs`** - File System
The `std::fs` module provides functions for interacting with the file system. You can read from and write to files, as well as work with directories.

- **Commonly Used Functions and Types:**
  - **`File::open()`**: Opens a file for reading.
  - **`File::create()`**: Creates a new file for writing.
  - **`read_to_string()`**: Reads the contents of a file into a `String`.
  - **`metadata()`**: Retrieves file or directory metadata (e.g., size, creation time).
  - **`remove_file()`**: Deletes a file.

```rust
use std::fs::File;
use std::io::{self, Read};

let mut file = File::open("hello.txt").expect("File not found");
let mut contents = String::new();
file.read_to_string(&mut contents).expect("Failed to read file");
println!("File contents: {}", contents);
```

### 3. **`std::collections`** - Data Structures
Rust’s standard library provides powerful collection types like `Vec`, `HashMap`, and `HashSet`, which are widely used for storing and manipulating data.

- **Commonly Used Types:**
  - **`Vec<T>`**: A growable array. It’s the most commonly used collection for dynamic arrays.
  - **`HashMap<K, V>`**: A hash map (key-value pairs), useful for storing data with a unique key.
  - **`HashSet<T>`**: A collection that stores unique values (like a mathematical set).
  - **`BTreeMap<K, V>`**: A sorted map, useful when order matters.

```rust
use std::collections::HashMap;

let mut map = HashMap::new();
map.insert("a", 10);
map.insert("b", 20);

if let Some(x) = map.get("a") {
    println!("Value: {}", x);
}
```

### 4. **`std::thread`** - Concurrency
Rust provides powerful tools for concurrency through threads. The `std::thread` module allows you to create and manage threads in your program.

- **Commonly Used Functions and Types:**
  - **`spawn()`**: Creates a new thread and runs the provided closure in that thread.
  - **`sleep()`**: Pauses the current thread for a specified amount of time.

```rust
use std::thread;
use std::time::Duration;

thread::spawn(|| {
    println!("Hello from a thread!");
});

thread::sleep(Duration::from_secs(1)); // Give time for thread to run
```

### 5. **`std::env`** - Environment Variables
The `std::env` module allows you to interact with environment variables and the operating system environment.

- **Commonly Used Functions and Types:**
  - **`var()`**: Retrieves the value of an environment variable.
  - **`args()`**: Returns the command-line arguments passed to the program.

```rust
use std::env;

let args: Vec<String> = env::args().collect();
println!("Arguments: {:?}", args);
```

### 6. **`std::cmp`** - Comparisons
The `std::cmp` module provides traits and functions for comparing values of types. It's essential when working with sorting, searching, or simply comparing values.

- **Commonly Used Functions and Traits:**
  - **`Ord`**: Trait for types that can be ordered (provides `cmp()`).
  - **`PartialOrd`**: Trait for types that can be partially ordered.
  - **`max()` and `min()`**: Return the maximum or minimum of two values.

```rust
use std::cmp::max;

let x = 5;
let y = 10;
println!("The maximum of {} and {} is {}", x, y, max(x, y));
```

### 7. **`std::option`** - Option Type
The `Option` type is used when there is a possibility of absence of a value. It's an enum that can either be `Some(T)` for a value of type `T`, or `None` for no value.

- **Commonly Used Variants and Functions:**
  - **`Some(T)`**: Contains a value.
  - **`None`**: Represents no value.
  - **`map()`**: Applies a function to the value inside `Some`.
  - **`unwrap()`**: Extracts the value from `Some`, panics if `None`.

```rust
let value = Some(10);
match value {
    Some(v) => println!("Got value: {}", v),
    None => println!("No value"),
}
```

### 8. **`std::result`** - Result Type
The `Result` type is used for functions that may return an error. It’s an enum with two variants: `Ok(T)` for success and `Err(E)` for errors.

- **Commonly Used Variants and Functions:**
  - **`Ok(T)`**: Contains a value of type `T` (success).
  - **`Err(E)`**: Contains an error of type `E`.
  - **`unwrap()`**: Extracts the value from `Ok`, panics if `Err`.
  - **`map()`**: Applies a function to the value inside `Ok`.

```rust
use std::fs::File;

let file = File::open("hello.txt");
match file {
    Ok(f) => println!("File opened: {:?}", f),
    Err(e) => println!("Error opening file: {}", e),
}
```

### 9. **`std::time`** - Time Operations
The `std::time` module provides functionality for working with time intervals and durations.

- **Commonly Used Types:**
  - **`Duration`**: Represents a time span.
  - **`Instant`**: A point in time, typically used for measuring elapsed time.

```rust
use std::time::{Duration, Instant};

let start = Instant::now();
thread::sleep(Duration::from_secs(2));
let elapsed = start.elapsed();
println!("Elapsed time: {:?}", elapsed);
```

### 10. **`std::process`** - Running External Processes
This module lets you spawn and manage child processes, such as running shell commands or external programs.

- **Commonly Used Functions:**
  - **`Command::new()`**: Starts a new process.
  - **`spawn()`**: Executes a command and returns a `Child` process.
  - **`status()`**: Waits for the child process to finish and returns its exit status.

```rust
use std::process::Command;

let output = Command::new("echo")
    .arg("Hello, world!")
    .output()
    .expect("Failed to execute command");

println!("Output: {}", String::from_utf8_lossy(&output.stdout));
```

---

### Conclusion

These modules are the core components that you'll use in most Rust programs, from simple applications to more complex systems. Here's a quick summary of what each one provides:

- **`std::io`**: Input/output functionality, including reading and writing from the console or files.
- **`std::fs`**: File system operations like reading, writing, and removing files.
- **`std::collections`**: Data structures like `Vec`, `HashMap`, and `HashSet`.
- **`std::thread`**: Concurrency through threads.
- **`std::env`**: Working with environment variables and command-line arguments.
- **`std::cmp`**: Comparing values, including maximum and minimum operations.
- **`std::option`**: The `Option` enum, used for handling optional values.
- **`std::result`**: The `Result` enum, used for functions that can return errors.
- **`std::time`**: Time-related operations.
- **`std::process`**: Running external processes.

	These modules form the backbone of most Rust programs. By familiarizing yourself with them, you'll be able to write powerful, efficient, and safe applications in Rust.