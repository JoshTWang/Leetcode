### Recursion

* **Recursion is an approach to solving problems using a function that calls itself as a subroutine.**
  *  The trick is that each time a recursive function calls itself, it reduces the given problem into subproblems.
  * The recursion call continues until it reaches a point where the subproblem can be solved without further recursion.

* 2 properties
  * **Base case** -- a terminating scenario that does not use recursion to produce an answer
  * **Recurrence relation** -- a set of rules that reduces all other cases towards the base case

###### Example - String reverse print

* O(*N*) space

```java
private static void printReverse(char [] str) {
  helper(0, str);
}

private static void helper(int index, char [] str) {
  if (str == null || index >= str.length) {
    return;
  }
  helper(index + 1, str);
  System.out.print(str[index]);
}
```

* O(1) space

```java
class Solution {
    public void reverseString(char[] s) {
      helper(0, s.length - 1, s);
    }

    private void helper(int start, int end, char [] s) {
      if (start >= end) {
        return;
      } 
      // swap between the first and the last elements.
      char tmp = s[start];
      s[start] = s[end];
      s[end] = tmp;
       
      helper(start + 1, end - 1, s);
   }
}
```

##### Recursion Function

In the function {F(X)}*F*(*X*), we will:

1. **Break the problem down into smaller scopes**, such as x0 ∈ X, x1 ∈ X, ..., xn∈X
2. Call function {F(x0)}, F(x1), ..., F(xn) ***recursively*** to solve the subproblems of {X}*X*;
3. Finally, process the results from the recursive function calls to solve the problem corresponding to {X}*X*.

#### Recursion relation

* base case
* recurrence relation

#### Memoization

* To eliminate the **duplicate calculation**
* [Memoization](https://en.wikipedia.org/wiki/Memoization) is an optimization technique used primarily to **speed up** computer programs by **storing** the results of expensive function calls and returning the cached result when the same inputs occur again



### Complexity Analysis

* Tail Recursion
* Stack overflow

#### Time Complexity

* Given a recursion algorithm, its time complexity {\mathcal{O}(T)}O(*T*) is typically the product of the number of recursion **invocations** (denoted as R) and the time complexity of calculation (denoted as (O(*s*)) that incurs along with **each recursion call**:

![image-20220311151621495](/Users/morningstar/Library/Application Support/typora-user-images/image-20220311151621495.png)

###### printReverse

* printReverse(str) = printReverse(str[1...n]) + print(str[0])
* O(printReverse) = n * O(1) = O(n)

###### Fibonacci number

* f(n) = f(n - 1) + f(n - 2)
* In this case, it is better resort to the **`execution tree`**, which is a tree that is used to denote the execution flow of a recursive function in particular. Each node in the tree represents an invocation of the recursive function. Therefore, the total number of nodes in the tree corresponds to the number of recursion calls during the execution.
* O(2<sup>n</sup>)

###### Fibonacci number with memoization

* O(n)

#### Space complexity

##### Recursion related space

The recursion related space refers to the memory cost that is incurred directly by the recursion, *i.e.* the stack to keep track of recursive function calls. In order to complete a typical function call, the system allocates some space in the stack to hold three important pieces of information:

1. The **returning address** of the function call. Once the function call is completed, the program must know where to return to, *i.e.* the line of code after the function call.
2. The **parameters** that are passed to the function call. 
3. The **local variables** within the function call.

* For recursive algorithms, the function calls chain up successively until they reach a `base case` (*a.k.a.* bottom case). This implies that the space that is used for each function call is accumulated.

![img](https://assets.leetcode.com/uploads/2019/01/25/card_recursion_stack.png)

###### printReverse

* O(n)

###### stackOverflow

* It is due to recursion-related space consumption that sometimes one might run into a situation called [stack overflow](https://en.wikipedia.org/wiki/Stack_overflow), where the stack allocated for a program reaches its maximum space limit and the program crashes.

##### Non-recursion related space

* As suggested by the name, the non-recursion related space refers to the memory space that is not directly related to recursion, which typically includes the space (normally in **heap**) that is allocated for the **global variables**.

###### Fibonacci Number -- memoization

* HashMap

##### Tail Recursion

* **Tail recursion** is a recursion where the recursive call is the final instruction in the recursion function. And there should be only **one** recursive call in the function.
* The benefit of having tail recursion is that it could avoid the accumulation of stack overheads during the recursive calls, since the system could reuse a fixed amount space in the stack for each recursive call. 

###### tail with non-tail

```java
public class Main {
    
  private static int helper_non_tail_recursion(int start, int [] ls) {
    if (start >= ls.length) {
      return 0;
    }
    // not a tail recursion because it does some computation after the recursive call returned.
    return ls[start] + helper_non_tail_recursion(start+1, ls);
  }

  public static int sum_non_tail_recursion(int [] ls) {
    if (ls == null || ls.length == 0) {
      return 0;
    }
    return helper_non_tail_recursion(0, ls);
  }

  //---------------------------------------------

  private static int helper_tail_recursion(int start, int [] ls, int acc) {
    if (start >= ls.length) {
      return acc;
    }
    // this is a tail recursion because the final instruction is the recursive call.
    return helper_tail_recursion(start+1, ls, acc+ls[start]);
  }
    
  public static int sum_tail_recursion(int [] ls) {
    if (ls == null || ls.length == 0) {
      return 0;
    }
    return helper_tail_recursion(0, ls, 0);
  }
}
```



#### Tips

* When in double, write down the **recurrence relationship**
  * mathematical forulas
* Whenever possible, apply memoization
  * avoid duplicate calculation
* When stack overflows, tail recursion might come to help