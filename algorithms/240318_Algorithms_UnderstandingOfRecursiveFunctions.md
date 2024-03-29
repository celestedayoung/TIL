# Understanding of Recursive Functions

## ✓ What is Recursive Functions in Programming?

Recursive functions in programming is a function which references itself.

## ✓ How to Engage in Inductive Reasoning?

### Example: Doninoes

If asked to explain why all the dominoes fall when the first one is toppled, there are two main approaches. For convenience, let's label the dominoes as 1, 2, ..., starting from the first one.

The first explanation method is straightforward, describing a chain reaction: when domino 1 falls, it knocks over domino 2, which in turn knocks over domino 3, and so on, until all dominoes have fallen.

On the other hand, the second explanation method employs mathematical induction. It states that "domino 1 falls," and "if domino k falls, then domino k+1 falls." Since these statements are true, it concludes that all dominoes fall. In fact, the reason why this second method is correct ultimately lies in the chain reaction process: domino 1 falls, then domino 2 falls, and so forth, leading to the falling of all dominoes.

However, going forward, one should think only up to "domino 1 falls" and "if domino k falls, then domino k+1 falls," before immediately reaching the conclusion that all dominoes fall.

```java
public void func(int n) {
    if (n == 0) return;
    System.out.print(n + " ");
    func(n - 1);
}
```

### Procedural Thinking

If you approach the problem with a procedural thinking, you can follow the flow of execution of the code. When `func(3)` is called, it prints 3 and then calls `func(2)`. `func(2)` prints 2 and then calls `func(1)`. `func(1)` prints 1 and then calls `func(0)`. Finally, `func(0)` encounters the `if (n == 0)` condition on line 2 and returns without further recursion. Following this process, when `func(3)` is executed, it prints 3, 2, 1, hence resulting in the output "3 2 1".

### Inductive reasoning

To understand that `func` prints numbers from `n` to 1 inductively, let's break it down:

1. First, it's evident that `func(1)` prints 1. This is straightforward.

2. Now, the crucial part is showing that if `func(k)` prints `k` to 1 in sequence, i.e., if it works for `k`, then it will also work for `k+1`, printing `k+1` to 1.

To demonstrate this, consider what happens when `func(k+1)` is called. After printing `k+1`, `func(k)` is called. Since we assume that `func(k)` prints `k` to 1 correctly, `func(k+1)` will indeed print `k+1` to 1 in sequence. These two statements being true, it is then inductively inferred that `func` prints numbers from `n` to 1 in sequence.

## ✓ Condition of a Recursive Function

- It should terminate without calling itself for certain inputs. → base condition
- All inputs should converge to a base condition.

If either of these two conditions is not met, the recursive function will fail to produce a result and will infinitely recurse, eventually causing a runtime error.

## ✓ Before Using Recursive Functions...

- Firstly, in recursion, one must clearly define the function. Definition entails specifying what the function will take as arguments and up to what point it will calculate before passing control back to itself.

- Furthermore, every recursive function can be implemented without recursion by using only loops to achieve the same behavior.

- Recursion, while making code concise when used appropriately, incurs significant overhead due to the cost of function calls in terms of memory and time. Therefore, if there is no significant difficulty in implementing the solution without recursion, it is preferable to use loops instead, considering the memory and time trade-off. However, for some problems where implementing without recursion leads to excessively complex code, using recursion is advisable.

- When a recursive function calls itself, information about the function accumulates in the stack area of memory. When solving problems, there's often a memory limit to consider. Sometimes, the stack memory is limited separately from the overall memory limit of the problem. If you're solving a problem in a context where stack memory is limited and your solution involves deep recursion, you may have to resort to iterative solutions instead. Note that local variables also occupy stack memory.

## ✓ Solving a Problem with a Recursive Function

[BOJ 1074](https://www.acmicpc.net/problem/1074)

In this problem, the numbering is done by dividing the array into four quadrants and proceeding in the order of 1, 2, 3, 4. Within each quadrant, the movement follows the pattern for N = 2. Therefore, the location with r = 2 and c = 2 is visited as the 12th position.

Now, let's determine the position for r = 6 and c = 2. Before visiting this location, all cells within quadrants 1 and 2 must have been visited. Thus, before quadrant 3 begins, 32 cells have already been visited. Within quadrant 3, the current cell we are considering is visited as the 12th position. Therefore, the final position is 32 + 12 = 44.

By observing the results for N = k, we can derive the results for N = k+1. This suggests a recursive approach to solve the problem.

```java
static int zFunction(int n, int r, int c) {

        // base condition
        if (n == 0) return 0;

        int half = (int)Math.pow(2, n - 1);

        if (r < half && c < half) return zFunction(n - 1, r, c);
        if (r < half && c >= half) return half * half + zFunction(n - 1, r, c - half);
        if (r >= half && c < half) return 2 * half * half + zFunction(n - 1, r - half, c);

        return 3 * half * half + zFunction(n - 1, r - half, c - half);
    }
```

1. function definition: A function that returns the order of visiting (r, c) in a 2<sup>n </sup> \* 2<sup>n</sup> array.
2. base condition: return 0 when n = 0.
3. recursive rules:
   - If (r, c) is in quadrant 1, return zFunction(n - 1, r, c).
   - If (r, c) is in quadrant 2, return half \* half + zFunction(n - 1, r, c - half).
   - If (r, c) is in quadrant 3, return 2 _ half _ half + zFunction(n - 1, r - half, c).
   - If (r, c) is in quadrant 4, return 3 _ half _ half + zFunction(n - 1, r - half, c - half).  
     (Note: "half" refers to the size of each quadrant, i.e., 2<sup>(n-1)</sup> \* 2<sup>(n-1)</sup>)

<details>
<summary>code</summary>
<div markdown="1">

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static int N, r, c;

    public static void main(String[] args) throws IOException {

        st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        r = Integer.parseInt(st.nextToken());
        c = Integer.parseInt(st.nextToken());

        System.out.println(zFunction(N, r, c));
    }

    // Recursive Function
    static int zFunction(int n, int r, int c) {

        // base condition
        if (n == 0) return 0;

        int half = (int)Math.pow(2, n - 1);

        if (r < half && c < half) return zFunction(n - 1, r, c);
        if (r < half && c >= half) return half * half + zFunction(n - 1, r, c - half);
        if (r >= half && c < half) return 2 * half * half + zFunction(n - 1, r - half, c);

        return 3 * half * half + zFunction(n - 1, r - half, c - half);
    }
}
```
</div>
</details>

---

### reference

https://en.wikipedia.org/wiki/Recursion_(computer_science)  
https://blog.encrypted.gg/943
