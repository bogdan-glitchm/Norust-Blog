---
date: 2026-11-11
categories:
- C++
- Memory Management
links:
    - C++ Reference:
        - std::array<T, N>: https://en.cppreference.com/cpp/container/array
---

# C++ Arrays

## Overview

C++ Arrays, `std::array<typename T, size_t N>`, are arrays that remain statically bounded in size, and that contain the size within them.

Using `std::array` reduces the chance of OOB accesses by transporting the size itself, and reduces the severity of OOB accesses when using `.at()`.

<!-- more -->

## Usage

C++ Arrays can be used after including the `<array>` header.

### Basic Example

```cpp
#include <array>

int main() {
    std::array<int, 5> data{};

    data[0];  // 0
    data[10];  // !! May read garbage data; This is UB!

    data.at(0);  // 0
    data.at(10);  // Throws std::out_of_range safely, preventing OOB access
}
```
