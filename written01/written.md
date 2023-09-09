# Written Assignment 1

1. Suppose that a size $n$ array is already sorted, but we don’t know that, and
   if we perform selection sort on it, there would be $n^2$ actions done. To
   explain this, when a selection sort algorithm is applied, we start at the
   first number in the array as the current index and then integrate through
   the rest of the remaining array to find a smaller number. If we can, we swap
   them with the current index, then move on with setting the current index to
   the next index in the array until we reach the end of it. Despite the array
   being sorted, since we don't know that detail when performing the algorithm,
   meaning we still have to perform the same amount of actions as if the array
   is not sorted, which is $n \cdot (n - 1) \cdot (n - 2) \cdot \ldots \cdot 1$.
   That would eventually simplify to $n^2$.

2. `curMin` is the minimum value of the array `arr` from index `0` to index `i`,
   and `curIndex` contains the index of that minimum value. That is a *loop
   invariant*, because both `curMin` and `curIndex` updates each time when `i`
   increments and when `arr[i]` satisfy the condition of `arr[i] < curMin`.
   With that being said, we check the value of `curMin` and `curIndex` for every
   iteration of the loop. Thus, there won't be any cases where they won't be
   forced to the corresponding value.

3. To find out what the first $n$ for which Algorithm A is faster, we need to
   find the first whole number of n after when B surpasses A. To explain this,
   we need to find out when algorithm B passes A, meaning A is more efficient
   than B when n goes towards $\infty$.

   To solve for $n$:
   $$A(n) = B(n)$$ $$50n^2 = 2^n$$

   I made a simple C program:

   ```c
    #include <stdio.h>
    #include <math.h>

    int main(int argc, char **argv)
    {
            int a = 0;
            int b = 0;
            for(int n = 1;; n++) {
                    a = 50 * pow(n, 2);
                    b = pow(2, n);
                    printf("n = %d, A = %d, B = %d\n", n, a, b);
            }

            return 0;
    }

   ```

   and here is the output:

   ```
   n = 1, A = 50, B = 2
   n = 2, A = 200, B = 4
   n = 3, A = 450, B = 8
   n = 4, A = 800, B = 16
   n = 5, A = 1250, B = 32
   n = 6, A = 1800, B = 64
   n = 7, A = 2450, B = 128
   n = 8, A = 3200, B = 256
   n = 9, A = 4050, B = 512
   n = 10, A = 5000, B = 1024
   n = 11, A = 6050, B = 2048
   n = 12, A = 7200, B = 4096
   n = 13, A = 8450, B = 8192
   n = 14, A = 9800, B = 16384
   n = 15, A = 11250, B = 32768
   n = 16, A = 12800, B = 65536
   n = 17, A = 14450, B = 131072
   n = 18, A = 16200, B = 262144
   n = 19, A = 18050, B = 524288
   n = 20, A = 20000, B = 1048576
   n = 21, A = 22050, B = 2097152
   n = 22, A = 24200, B = 4194304
   n = 23, A = 26450, B = 8388608
   n = 24, A = 28800, B = 16777216
   n = 25, A = 31250, B = 33554432
   n = 26, A = 33800, B = 67108864
   n = 27, A = 36450, B = 134217728
   n = 28, A = 39200, B = 268435456
   n = 29, A = 42050, B = 536870912
   n = 30, A = 45000, B = 1073741824
   ...
   ```

   As shown in the program's output, at $n = 14$, algorithm A surpasses Algorithm
   B.

4. Table

    |                        | $\in O(\sqrt{n})$ | $\in O(n)$ | $\in O(n \log(n))$ | $\in O(1)$ | $\in O(n^3)$ | $\in O(\log^2(n))$ | $\in O(3^n)$ | $\in O(\log(n))$ |
    |------------------------|-------------------|------------|--------------------|------------|--------------|--------------------|--------------|------------------|
    | $2^n$                  |                   |            |                    |            |              |                    | &check;      |                  |
    | $4n^2 + \log(n)$       |                   |            |                    |            | &check;      |                    | &check;      |                  |
    | $3^{n+1}$              |                   |            |                    |            |              |                    | &check;      |                  |
    | $n^2 \log(n)$          |                   |            |                    |            | &check;      |                    | &check;      |                  |
    | $\sqrt{n} + 2 \log(n)$ | &check;           |            | &check;            |            | &check;      | &check;            | &check;      |                  |
    | $984$                  | &check;           | &check;    | &check;            | &check;    | &check;      | &check;            | &check;      | &check;          |
    | $6 \log(n) + 2$        | &check;           | &check;    | &check;            |            | &check;      | &check;            | &check;      | &check;          |

5. One example such function is $f(n) = \log{(n)}$.

   $f(n) \in O(n)$, because logarithmic function grows much slower than the
   square root function, such that $\log{(n)} \le c \sqrt{n}$ for some positive
   constant $c$ and all sufficiently large $n$. Therefore, $f(n) \in O(n)$.

   On the other hand, $f(n) \notin \Omega{(n)}$, because there is no
   constant $c$ such that $\log{(n)} \ge c \sqrt{n}$.

6. To break down the algorithm, there is one nested loop in it:
   1. the outer loop runs for every other item in the array starting from the
      beginning of the array, assuming there are n items in the array, the loop
      will run approximately $\frac{n}{2}$ times.

   2. For each outer loop, the innner loop also runs for every other item in the
      array starting from the second item within the array. Therefore, the inner
      loop would run approximately $\frac{n}{2}$ times as well.

   From there, we can get the running time of the algorithm by multiplying the
   running time of two inner loops, which we get:

   $$(\frac{n}{2})^2 = \frac{n^2}{4}$$

   Hence, the complexity of the algorithm is $n^2$.

7. The given function takes an array with arbitrary amount of integer numbers.
   There is a nested loop. The outer loop starts from the second element of the
   array, and interate until the end of the array. For each time outer loop
   excutes, the inner loop does the same thing interating through the whole
   array. For each time of the whole interation, sum up the index value of the
   outer loop multiply the inner loop.

   To evaluate the computational complexity, we'll focus on the nested loop to
   see how many times the innter most statement (`sum = sum + arr[i * j]`), so
   called action happens:

   For i = 1, the inner loop runs `arr.length - 1` times.
   For i = 2, the inner loop runs `(arr.length - 1) / 2` times.
   For i = 3, the inner loop runs `(arr.length - 1) / 3` times.
   For i = k, the inner loop runs (arr.length - 1) / k times.
   ...

   Given this progression, the total number of times the inner-most statement is
   executed is:
   $$Total = (arr.length) \times (1 + \frac{1}{2} + \frac{1}{3} + \ldots +
   \frac{1}{arr.length - 1})$$

   The series inside the parentheses is a harmonic series. Given the provided
   inequalities:
   $$\ln{(n)} + \frac{1}{n} \le 1 + \frac{1}{2} + \frac{1}{3} + \ldots +
   \frac{1}{n} \le \ln{(n)} + 1$$
   $$\ln(n) + \frac{1}{n} \leq \sum_{i=1}^{n} \frac{1}{i} \leq \ln(n) + 1$$
   $$\ln(arr.length - 1) + \frac{1}{arr.length - 1} \leq
   \sum_{i=1}^{arr.length - 1} \frac{1}{i} \leq \ln(arr.length - 1) + 1$$

   Thus, when we factor in the multiplication by `arr.length − 1`, it confirms
   the computational complexity to be $O(n \log{(n)})$ where $n$ is the length
   of the array.

8. As described in the pseudocode for this algorithm, we are given a set $S$
   with an arbitrary amount of numbers. When recursing through, we let $s$ be
   the first element of the set $S$, then for each recursive step, the first
   element gets subtracted from the set $S$. The new set $S$ without its first
   element after the recursive step will be denoted as set $R$. To find all
   subsets of $R$, we recursively operate on set $R$ exactly as how set $S$ was
   operated on previously, until we hit the base case, in which set $R$ is
   empty. After set $R$ is empty, we create another new set $S_{1}$ to hold all the
   subsets that have been generated by the recursive calls. Since we hit the
   base case, a function return is triggered and the top frame on the call stack
   gets popped, and so on for the rest of the frames on the call stack. Each
   time the stack frame gets popped, we add the subset from the previous
   recursive calls to set $S_{1}$, and finally we return the set $S_{1}$.

   A detailed recursive tree can be found ![here](tree.png).
