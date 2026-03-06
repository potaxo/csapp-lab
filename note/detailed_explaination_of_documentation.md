### Restating your question

You want **examples of good documentation and comments in real code**, following the guidelines you showed (file headers, function headers, comments explaining *why*, etc.), using languages like **C, Java, and Rust**.

Below are practical examples similar to what you might see in **university projects or open-source repositories**.

---

# 1. File Header Example

## C Example

```c
/*
 * file: hashmap.c
 * author: potaxo
 * email: potaxo@example.com
 *
 * This file implements a simple hash map used by the caching subsystem
 * of the project. It provides insertion, lookup, and deletion operations
 * with average O(1) time complexity.
 *
 * The hash map is used by cache.c to store key-value pairs of HTTP
 * responses so they can be retrieved quickly without recomputation.
 */
```

Key ideas:

* Explains **purpose of file**
* Explains **how it fits into project**
* Includes **author information**

---

# 2. Function Header Example

## C Example

```c
/**
 * Inserts a key-value pair into the hash map.
 *
 * Parameters:
 *   map  - pointer to the hash map structure
 *   key  - string key to insert
 *   value - pointer to value associated with the key
 *
 * Returns:
 *   0 on success
 *   -1 if the map is full or memory allocation fails
 *
 * Side Effects:
 *   May allocate memory for a new entry.
 */
int hashmap_insert(HashMap *map, const char *key, void *value) {
    int index = hash(key) % map->capacity;
    map->table[index] = value;
    return 0;
}
```

Important points:

* Explains **purpose**
* Lists **parameters**
* Lists **return values**
* Describes **side effects**

---

# 3. Large Block Comment Example

Sometimes code is long and complex.

```c
/*
 * Resize the hash map when the load factor becomes too large.
 *
 * Strategy:
 * 1. Allocate a new table with double capacity.
 * 2. Rehash all existing keys into the new table.
 * 3. Free the old table.
 *
 * This operation is expensive (O(n)), but it happens rarely
 * and keeps average lookup time constant.
 */
void hashmap_resize(HashMap *map) {
    ...
}
```

This helps the reader **understand the algorithm before reading the code**.

---

# 4. Tricky Code Example

Pointer arithmetic often needs explanation.

```c
char *buffer_end = buffer + size;

/* 
 * Move the pointer until we hit the first newline.
 * Pointer arithmetic is used here to avoid copying memory.
 */
while (buffer < buffer_end && *buffer != '\n') {
    buffer++;
}
```

Good comment:

* Explains **why pointer arithmetic is used**
* Helps future readers understand intent.

---

# 5. Java Example (Typical Style)

Java uses **Javadoc** comments.

```java
/**
 * Computes the average value of an integer array.
 *
 * @param numbers array of integers
 * @return average value of the array
 * @throws IllegalArgumentException if the array is empty
 */
public static double average(int[] numbers) {
    if (numbers.length == 0) {
        throw new IllegalArgumentException("Array cannot be empty");
    }

    int sum = 0;
    for (int n : numbers) {
        sum += n;
    }

    return (double) sum / numbers.length;
}
```

Javadoc tools can automatically generate **HTML documentation**.

---

# 6. Rust Example (Rustdoc Style)

Rust documentation comments use `///`.

```rust
/// Calculates the factorial of a number.
///
/// # Arguments
///
/// * `n` - The number to compute the factorial for.
///
/// # Returns
///
/// The factorial of `n`.
///
/// # Panics
///
/// Panics if `n` is negative.
fn factorial(n: u64) -> u64 {
    (1..=n).product()
}
```

Rust can generate docs with:

```bash
cargo doc --open
```

---

# 7. Example of **Bad vs Good Comments**

## Bad

```c
// increment i
i++;
```

This is useless because the code already says that.

---

## Good

```c
// Skip the header row because it contains column names
i++;
```

This explains **why** the increment happens.

---

# Summary

Good documentation usually includes:

| Type                | Purpose                               |
| ------------------- | ------------------------------------- |
| File header         | explain role in project               |
| Function header     | explain inputs, outputs, side effects |
| Large block comment | explain algorithm or workflow         |
| Tricky code comment | explain non-obvious logic             |

And most importantly:

> Comments should explain **WHY**, not **WHAT**.

---

💡 **Forward-thinking tip**

Professional engineers often follow the **“self-documenting code + minimal comments” rule**:

1. Use clear names

   ```
   totalPrice
   computeChecksum()
   readConfigFile()
   ```

2. Write comments only when **the reasoning isn't obvious**.

If you want, I can also show you **real examples from Linux kernel code or Git source code**, which are some of the best real-world C documentation styles.
