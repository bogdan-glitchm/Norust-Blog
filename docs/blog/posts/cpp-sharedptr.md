---
date: 2026-11-11
categories:
- C++
- Memory Management
links:
    - C++ Reference:
        - std::shared_ptr<T>: https://en.cppreference.com/cpp/memory/shared_ptr
        - std::make_shared<T>: https://en.cppreference.com/cpp/memory/shared_ptr/make_shared
        - std::make_shared_for_overwrite<T>: https://en.cppreference.com/cpp/memory/shared_ptr/make_shared
---

# C++ Shared Pointers

## Overview

C++ Shared Pointers, `std::shared_ptr<T>`, can be used when multiple sections of your codebase need to handle the same data.

An important feature of `std::shared_ptr<T>` is its reference counting &mdash; it will automatically deallocate its memory, but only when all instances of shared pointers pointing to that memory have been destroyed.

<!-- more -->

## Usage

Shared pointers can be used after including the `<memory>` header.

### Basic Example

```cpp
#include <memory>

void increment(std::shared_ptr<int> value) {
    // value is guaranteed to be valid
    *value += 1;

    // value is destroyed here
}

int main() {
    std::shared_ptr<int> a = std::make_shared<int>(30);
    
    {
        std::shared_ptr<int> b = a;
        increment(b);

        // b is destroyed here
    }

    // a is destroyed here
    // the memory is deallocated here
    return 0;
}
```

### Arrays

Shared pointers include special overloads for **arrays**. Keep in mind, however, that they **do not store the size**.

```cpp
#include <memory>

void increment(int size, std::shared_ptr<int[]> value) {
    // value is guaranteed to be valid
    for (int i = 0; i < size; i++) {
        value[i] += 1;
    }

    // value is destroyed here
}

int main() {
    std::shared_ptr<int[]> a = std::make_shared<int[]>(3);  // size=3
    for (int i = 0; i < 3; i++) {
        a[i] = i + 1;  // make the values be {1, 2, 3}
    }
    
    {
        std::shared_ptr<int[]> b = a;
        increment(3, b);

        // b is destroyed here
    }

    // a is destroyed here
    // the memory is deallocated here
    return 0;
}
```
