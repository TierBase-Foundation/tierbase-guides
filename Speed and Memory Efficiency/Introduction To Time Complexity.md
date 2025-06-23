# Introduciton To Time Complexity {#introduction-to-time-complexity}

In competitive programming contests, programs are required to run within a certain time limit. In the [USACO (USA Computing Olympiad)](https://usaco.org), a typical time limit for a problem is $2$ seconds for $\text{C}$ or $\text{C++}$, and $4$ seconds for $\text{Java}$ and $\text{Python}$. 


Using a specific number to represent how fast a program runs just doesn't work. For example,
- The time it takes to run a program varies across computers and programming languages.
  - Even on the same computer, the same code can run a few milliseconds faster or slower.
- The speed of the code can scale with input size.
  - When debugging, it is very hard to tell which piece of code is the bottleneck, because some parts of your code can scale faster than other parts of the code. 

How can we address this problem? With [Big O notation](./Notations#big-o-notation), [Big $\Omega$ notation](./Notations#big-omega-notation), and [Big $\Theta$ notation](./Notations#big-theta-notation).