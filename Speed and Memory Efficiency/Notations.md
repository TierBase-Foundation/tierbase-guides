# Notations {#notations}

There are three main types of notation to accurately represent the speed of a program - [Big O notation](./Notations#big-o-notation), [Big $\Omega$ notation](./Notations#big-omega-notation), and [Big $\Theta$ notation](./Notations#big-theta-notation).

## Big O Notation {#big-o-notation}

Big O notation represents the speed of a program as $O(f(n))$, where $f(n)$ is a function on $n$. $O(f(n))$ denotes the upper bound (worst-case scenario) of how many operations will happen in the program, given $n$ as the input size. Competitive programming focuses on Big O notation, because analyzing the runtime of a program in Big O notation ensures that no test case (particularly cases with $n=0$, $1$, or $2 \cdot 10^5$) results in a Time Limit Exceeded (TLE) verdict.

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

Unlike Big O notation, big Omega notation represents the speed of a program as $\Omega(f(n))$, where $f(n)$ is a function on $n$. $\Omega(f(n))$ denotes the lower bound (best case scenario) of how many operations will happen in the program, given $n$ as the input size.

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

Big Theta notation represents the speed of a program as $\Theta(f(n))$, where $f(n)$ is a function on $n$. $\Theta(f(n))$ approximates the average number of operations occuring in the program, given $n$ as the input size. In other words, $\Theta(f(n))$ states that the algorithm's performance grows at the same rate as the function $f(n)$.

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

Sometimes, a program can exceed time limits despite having the intended time complexity. This is due to constant factors. Even though constant factors are omitted from the time complexity of a program, they still have an impact on the overall runtime.

For example, consider the following two code snippets:
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
The second piece of code generally runs $2$ times faster than the first, because it iterates over all unordered pairs of integers -- $(a, b)$ is the same as $(b, a)$.

### Approximating The Intended Time Complexity {#approximating-the-intended-time-complexity}

In all competitive programming problems, there are constraints on $n$, $m$, and similar variables. For instance, [the problem](https://usaco.org/index.php?page=viewproblem2&cpid=1347) states that $1 \le n, m \le 2 \cdot 10^5$, meaning that the input will only have $n$ and $m$ within the range $1$ to $2 \cdot 10^5$.

Using these constraints, and the fact that typical grading servers can perform roughly $10^8$ operations every second, we can approximate the required time complexity of the program with the table below.

TODO

### Amortized Analysis (Main Article: [Amortized Analysis](./Amortized%20Analysis)) {#amortized-analysis}

When we talk about the time complexity of an algorithm, we usually think about how it performs for a single input. However, many problems such as [this one](https://usaco.org/index.php?page=viewproblem2&cpid=1494) introduce a variable $T$ that represents the number of test cases for each input. Surface-level thinking may find that the time complexity would be $O(T \cdot n_{\text{max}})$, where $n_{\text{max}}$ is the maximum possible input size for any single test case. However, the majority of these problems explicitly state a constraint on the sum of $n$ over all test cases, rather than just the maximum $n$ for a single test case.

In the above example problem, it mentions that <i>It is guaranteed that the sum of $n$ over all test cases does not exceed $10^6$</i>. As a result, the intended solution has a time complexity of $O(n)$ instead of $O(T \cdot n_{\text{max}})$, meaning that the total number of operations over all $T$ test cases within a single input is at most $n=10^6$, not $T \cdot n_{\text{max}} = 100 \cdot 10^6 = 10^8$.

These problems are the most simple example of [amortized analysis](./Amortized%20Analysis), where instead of analyzing the worst-case for each individual operation or test case and multiplying, we look at the total cost over a sequence of operations or test cases.