# Introduction To Time Complexity {#introduction-to-time-complexity}

In competitive programming contests, programs are required to run within a certain time limit. In the [USACO (USA Computing Olympiad)](https://usaco.org), a typical time limit for a problem is $2$ seconds for $\text{C}$ or $\text{C++}$, and $4$ seconds for $\text{Java}$ and $\text{Python}$. 


Using a specific number to represent how fast a program runs just doesn't work. For example,
- The time it takes to run a program varies across computers and programming languages.
  - Even on the same computer, the same code can run a few milliseconds faster or slower.
- The speed of code can scale with input size.
  - As input size grows, some parts of your code might become much slower than others. When debugging, this makes it difficult to pinpoint the bottleneck in your program - a section of code that is limiting your program's overall speed.

How can we address this problem? Rather than representing the speed a program with a fixed number, we can express time complexity as a function on input size and describe how the number of operations in the program scales with the input size -- using [Big O notation](./Notations#big-o-notation), [Big $\Omega$ notation](./Notations#big-omega-notation), and [Big $\Theta$ notation](./Notations#big-theta-notation).