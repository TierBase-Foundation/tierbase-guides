# Notations {#notations}

There are three main types of notation to describe the time complexity of a program - [Big O notation](./Notations#big-o-notation), [Big $\Omega$ notation](./Notations#big-omega-notation), and [Big $\Theta$ notation](./Notations#big-theta-notation).

## Big O Notation {#big-o-notation}

Big O notation represents the time complexity of a program as $O(f(n))$, where $f(n)$ is a function on $n$. $O(f(n))$ denotes the <b>upper bound</b> (worst-case scenario) of how many operations will happen in the program, given $n$ as the input size. Competitive programming focuses on Big O notation, because analyzing the runtime of a program in Big O notation ensures that no test case (particularly cases with $n=0$, $1$, or very large values of $n$) results in a Time Limit Exceeded (TLE) verdict.

<br>

As an example of Big O notation, consider the following piece of code:
```c++
for (int i = 0; i < n; i++) {
    cout << i << "\n";
}
```
```java
for (int i = 0; i < n; i++) {
    System.out.println(i);
}
```
```python
for i in range(0, n): 
    print(i)
```
The $\text{for}$ loop calls the output operation $n$ times. In this case, $f(n)=n$, and the time complexity of the code in Big O notation is $O(f(n)) = O(n)$.

<br>

Sometimes, if multiple variables are introduced, the function $f$ takes in more variables. For example, consider the following piece of code: 
```c++
for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
        cout << i << ", " << j << "\n";
    }
}
```
```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
        System.out.println(i + ", " + j);
    }
}
```
```python
for i in range(0, n): 
    for j in range(0, m): 
        print(str(i) + ", " + str(j))
```
In each inner $\text{for}$ loop, the output operation is called $m$ times, and in each outer $\text{for}$ loop, the inner $\text{for}$ loop is called $n$ times. Therefore, $f(n, m) = nm$, and the time complexity of the code in Big O notation is $O(nm)$.

<br>

## Big Omega Notation {#big-omega-notation}

Big Omega notation represents the time complexity of a program as $\Omega(f(n))$, where $f(n)$ is a function on $n$. Unlike Big O notation, $\Omega(f(n))$ denotes the <b>lower bound</b> (best case scenario) of how many operations will happen in the program, given $n$ as the input size.

For instance, consider the following search algorithm for an element in a list:
```c++
int find_element_with_value(int value) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == value) {
            return i;
        }
    }
    return -1;
}
```
```java
public int find_element_with_value(int value) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == value) {
            return i;
        }
    }
    return -1;
}
```
```python
def find_element_with_value(value):
    for i in range(0, n):
        if (arr[i] == value):
            return i

    return -1
```
The best case scenario is when the element would be found at the first position of the list. So, $f(n) = 1$ and the time complexity in Big Omega notation is $\Omega(f(n)) = \Omega(1)$.

## Big Theta Notation {#big-theta-notation}

Big Theta notation represents the time complexity of a program as $\Theta(f(n))$, where $f(n)$ is a function on $n$. $\Theta(f(n))$ approximates the <b>average number</b> of operations occuring in the program, given $n$ as the input size. In other words, $\Theta(f(n))$ states that the algorithm's performance grows at the same rate as the function $f(n)$.

Consider the previous example:
```c++
int find_element_with_value(int value) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == value) {
            return i;
        }
    }
    return -1;
}
```
```java
public int find_element_with_value(int value) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == value) {
            return i;
        }
    }
    return -1;
}
```
```python
def find_element_with_value(value):
    for i in range(0, n):
        if (arr[i] == value):
            return i

    return -1
```
On average, the function loops through half of the elements in the list as opposed to the full length. However, rather than having a time complexity of $\Theta\left(\frac{n}{2}\right)$, the function still has a time complexity of $\Theta(n)$, because [constant factors](./Constant%20Factors) are ignored when analyzing time complexity. 

## Notes {#notes}

### Constant Factors (Main Article: [Constant Factors](./Constant%20Factors)) {#constant-factors}

When analyzing algorithms, time complexity helps us understand how the runtime grows with input size. However, the actual performance can still differ due to constant factors, which aren't represented in big O, big Omega, or big Theta notation.

As an example, a program may call $100n^2 + 5n + 30$ operations at worst, which is simplified to $O(n^2)$ in its time complexity (ignoring constants such as coefficients $100$ and lower-order terms $5n$ and $30$). But in practice, these constants can impact a program's speed, possibly making one $O(n^2)$ algorithm noticeably slower than another and leading to a time limit exceeded verdict (TLE). 

The following two pieces of code have the same time complexity $O(n)$, but they differ in their actual runtime due to constant factors.
```c++
int sum = 0;
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < n; j++) {
        sum += i * j;
    }
}
cout << sum << endl;
```
```java
int sum = 0;
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < n; j++) {
        sum += i * j;
    }
}
System.out.println(sum);
```
```python
sum = 0
for i in range(0, 10):
    for j in range(0, n):
        sum += i * j
print(sum)
```

```c++
int sum = 0;
for (int j = 0; j < n; j++) {
    sum += j;
}
cout << sum << endl;
```
```java
int sum = 0;
for (int j = 0; j < n; j++) {
    sum += j;
}
System.out.println(sum);
```
```python
sum = 0
for j in range(0, n):
    sum += j
print(sum)
```
The first piece of code generally runs $10$ times slower than the second, because it iterates over the inner $\text{for}$ loop $10$ times, resulting in a total of $10n$ operations, rather than just $n$.

### Approximating The Intended Time Complexity {#approximating-the-intended-time-complexity}

In all competitive programming problems, there are constraints on $n$, $m$, and similar variables. For instance, [the problem](https://usaco.org/index.php?page=viewproblem2&cpid=1347) states that $1 \le n, m \le 2 \cdot 10^5$, meaning that the input will only have $n$ and $m$ within the range from $1$ to $2 \cdot 10^5$.

Using these constraints, and the fact that typical grading servers can perform roughly $10^8$ operations every second, we can approximate the required time complexity of the program with the table below. 

| Constraints on $n$ | Expected Time Complexity | Potential Algorithms / Data Structures Involved |
|---|---|---|
| $n \le 10^{18}$ | $O(1)$ or $O(\log{n})$ | $O(1)$: algebraic manipulation <br> $O(\log{n})$: binary search, digit DP (dynamic programming) |
| $n \le 10^6$ | $O(n)$ or $O(n\log{n})$ | $O(n)$: two pointers, depth-first search (DFS), breadth-first search (BFS), array, queue, stack, deque, unordered set, unordered map <br> $O(n\log{n})$: binary search, fast sorting algorithms (merge sort, quicksort, heap sort), Kruskal's algorithm, Prim's algorithm, Dijkstra's algorithm, priority queue, set, map, segment tree, binary indexed tree, order statistic tree, disjoint set union (DSU) |
| $n \le 2 \cdot 10^5$ | $O(n\sqrt{n})$ | $(n\sqrt{n})$: Mo's algorithm, square root decomposition, prime factorization |
| $n \le 8000$ | $O(n^2)$ | $O(n^2)$: naive sorting algorithms (bubble sort, insertion sort), 2D array |
| $n \le 500$ | $O(n^3)$ | $O(n^3)$: shortest path algorithms (Bellman-Ford, Floyd-Warshall, Modified Dijkstra), matrix multiplication |
| $n \le 80$ | $O(n^4)$ | $O(n^4)$: combination of previous algorithms and / or data structures |
| $n \le 40$ | $O(2^\frac{n}{2})$ | $O(2^\frac{n}{2})$: meet in the middle |
| $n \le 20$ | $O(2^n)$ | $O(2^n)$: generating subsets, bitmask DP |
| $n \le 10$ | $O(n!)$ | $O(n!)$: generating permutations |


TODO: Link data structures in table to actual articles / pages.


### Amortized Analysis {#amortized-analysis}

When we talk about the time complexity of an algorithm, we usually think about how it performs for a single input. However, many problems such as [this one](https://usaco.org/index.php?page=viewproblem2&cpid=1494) introduce a variable $T$ that represents the number of test cases for each input. Surface-level thinking may find that the time complexity of this problem would be $O(Tn)$ and the number of operations $T_\text{max} \cdot n_\text{max}=(100)(2 \cdot 10^5)=2 \cdot 10^7$ for each input. However, the majority of these problems explicitly state a constraint on the sum of $n$ over all test cases, rather than just the maximum $n$ for a single test case.

In the above example problem, it mentions that <i>It is guaranteed that the sum of $n$ over all test cases does not exceed $10^6$</i>. As a result, the intended solution has a time complexity of $O(n)$ instead of $O(Tn)$, meaning that the total number of operations over all $T$ test cases within a single input is at most $n=10^6$, not $T_\text{max} \cdot n_\text{max}=2 \cdot 10^7$.

These problems are the most simple example of [amortized analysis](./Runtime%20Analysis#amortized-analysis), where we consider the total cost across a sequence of operations rather than looking at the worst-case time complexity for a single operation and multiplying it by the number of operations. This approach is really helpful for us to understand and analyze programs where the time complexity of individual operations can vary a lot.