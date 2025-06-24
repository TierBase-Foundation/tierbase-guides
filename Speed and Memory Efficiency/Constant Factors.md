# Constant Factors {#constant-factors}

Sometimes, operations with the same time complexity don't take the exact same amount of time. This difference is due to constant factors.

As an example, consider the following two pieces of code:
```c++
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        cout << i << ", " << j << "\n";
    }
}
```
```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.println(i + ", " + j);
    }
}
```
```python
for i in range(0, n):
    for j in range(0, n):
        print(str(i) + ", " + str(j))
```

```c++
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
        cout << i << ", " << j << "\n";
    }
}
```
```java
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
        System.out.println(i + ", " + j);
    }
}
```
```python
for i in range(0, n):
    for j in range(i, n):
        print(str(i) + ", " + str(j))
```
Although both pieces of code have time complexity $O(n^2)$, the second piece of code generally runs $2$ times faster than the first, as it iterates over all <b>unordered</b> pairs of integers -- it treats $(a, b)$ as the same as $(b, a)$. 

## Definition {#definition}

Constant factors can be defined as fixed multipliers or additive terms in a program's execution time. While they are ignored in a program's time complexity, they still influence how long a program actually takes to run.

## Minimizing Constant Factors {#minimizing-constant-factors}

As the input size $n$ grows infinitely large, constant factors become negligible, but in settings with strict time limits, such as competitive programming, high, or simply "bad", constant factors can lead to a Time Limit Exceeded (TLE) verdict.

If you encounter a Time Limit Exceeded (TLE) verdict, you may be using data structures that have high constant factors and negatively impacts runtime. A few high constant factor data structures and algorithms are listed below:

C++:
- `std::map`: Ordered maps are typically implemented as a balanced binary search tree. Although the time complexity of each `std::map` operation (insert, find, and erase) is $O(\log(n))$, these operation involve pointer dereferences, node allocations, and rebalancing steps which add to the overhead and constant factor.
  - Consider hashing large data (e.g., `std::string`) into a fixed-size integer and using arrays for key lookups.
    - Warning: This method can result in <b>collisions</b> (false positives), where different data hashes to the same value. Learn more about how to avoid collisions at [this page](./Hashing#TODO).
  - Also consider `std::unordered_map` as an alternative data structure -- its operations take on average $O(1)$ time instead of $O(\log{n})$, but it doesn't maintain any sorted order. 

- `std::set`: Ordered sets are also usually implemented as a balanced binary search tree. See `std::map`.
  - Consider `std::unordered_set` as an alternative data structure -- its operations take on average $O(1)$ time instead of $O(\log{n})$, but it doesn't maintain any sorted order.

- `__gnu_pbds::tree`: Order statistic trees are also an extension of a balanced binary search tree. See `std::map`.

- `std::vector`: Dynamic arrays are a bit slower than static arrays. 
  - Consider opting for static arrays, which are faster especially with higher dimensions (for example, `int arr[8001][8001]` instead of `vector<vector<int>> arr`).

Java:
- `TreeMap`: Ordered maps are typically implemented as a balanced binary search tree. Although the time complexity of each `TreeMap` operation (put, get, and remove) is $O(\log(n))$, these operation involve pointer dereferences, node allocations, and rebalancing steps which add to the overhead and constant factor.
  - Consider hashing large data (e.g., `String`) into a fixed-size integer and using arrays for key lookups.
    - Warning: This method can result in <b>collisions</b> (false positives), where different data hashes to the same value. Learn more about how to avoid collisions at [this page](./Hashing#TODO).
  - Also consider `HashMap` as an alternative data structure -- its operations take on average $O(1)$ time instead of $O(\log{n})$, but it doesn't maintain any sorted order.

- `TreeSet`: Ordered sets are also usually implemented as a balanced binary search tree. See `TreeMap`.
  - Consider `HashSet` as an alternative data structure -- its operations take on average $O(1)$ time instead of $O(\log{n})$, but it doesn't maintain any sorted order.

- `ArrayList`: Dynamic arrays are a bit slower than static arrays. 
  - Consider opting for static arrays, which are faster especially with higher dimensions (for example, `int[][] arr` instead of `ArrayList<ArrayList<int>> arr`).

Python:
- Python is a highly optimized language, so data structures such as `dict`, `list`, and `tuple` have low constant factors for most operations, making them generally efficient for a wide range of use cases. 
- However, Python is in general slower than compiled languages such as Java and C++, making the language undesirable in competitive programming.

General:
- Although segment trees are much more versatile than binary indexed trees (BITs), they have a much higher constant factor than BITs.
  - Consider using a BIT over a segment tree if possible.
- Recursive functions have high constant factors.
  - Optimization 1: Dynamic programming (DP) helps by storing previously computed answers in a lookup table so redundant computation is avoided.
  - Optimization 2: If possible, opt for iterative DP instead of recursive DP to reduce the high constant factor of recursion, the possibility of a Time Limit Exceeded (TLE) verdict, and the possibility of a Stack Overflow error.

TODO: link above mentioned data structures with url