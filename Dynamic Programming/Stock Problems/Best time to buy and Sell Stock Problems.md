[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/#/description)

* We have one transaction, so the task is to find maximal difference between a **latter** stock price and an **earlier** one.

[122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/#/description)

* We can make as many as transactions as one would like, so the task is to capture **each** augmentation and avoid each plunging of stock price.

[123. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/#/description)

[188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/#/description)

* III and IV are similar -- At most 2 transactions vs. At most k transactions.

[309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/#/description)

* DP similar to house robber
* DP with State machine

[714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/contest/leetcode-weekly-contest-55/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

[New approach](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/discuss/75924/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems)



##### I - General cases

**Give an array representing the price of stocks on each day, what determines the maximum profit we can obtain.**

* `prices[]`: the stock price array of length n
* `i`: the `ith` day
* `k`: the maximum number of transactions allowed
* `T[i][k]` the maximum profit that could be gained at the end of the `ith` day with at most `k` transactions
* base cases: `T[-1][k] = T[i][0] = 0`



**Intuition**: relate `T[i][k]` to its subproblems like `T[i-1][k], T[i][k-1], T[i-1][k-1], ...`



##### Actions taken on the `ith` day

* **buy**, **sell**, **rest**

* if we decide to **buy** on the `i-th` day, there should be `0` stock held in our hand before we buy;
* if we decide to **sell** on the `i-th` day, there should be exactly `1` stock held in our hand before we sell.



We can split our dp into `T[i][k][0]` and `T[i][k][1]`

1. Base cases:
   `T[-1][k][0] = 0, T[-1][k][1] = -Infinity`
   `T[i][0][0] = 0, T[i][0][1] = -Infinity`

   

2. Recurrence relations:
   `T[i][k][0] = max(T[i-1][k][0], T[i-1][k][1] + prices[i])`
   `T[i][k][1] = max(T[i-1][k][1], T[i-1][k-1][0] - prices[i])`

---

##### II Applications to specific cases

* k = 1 transaction
* k = infinite transactions

* k = 2 transactions
* k transactions
* cooldown
* transaction fee

---



###### case I: k = 1

For this case, we really have two unknown variables on each day: `T[i][1][0]` and `T[i][1][1]`, and the recurrence relations say:

```java
T[i][1][0] = max(T[i-1][1][0], T[i-1][1][1] + prices[i])
T[i][1][1] = max(T[i-1][1][1], T[i-1][0][0] - prices[i]) 
					 = max(T[i-1][1][1], -prices[i])
```

where we have taken advantage of the base case`T[i][0][0] = 0` for the second equation. (Transaction == 0 which means that we can't do anything)

* If you notice that the maximum profits on the `i-th` day only depend on the `(i - 1)-th` day, the `O(n)` time and `O(1)` space solution is as follows:

```java
public int maxProfit(int[] prices) {
    int T_i10 = 0, T_i11 = Integer.MIN_VALUE;
        
    for (int price : prices) {
        T_i10 = Math.max(T_i10, T_i11 + price); // not holding
        T_i11 = Math.max(T_i11, -price); // holding
    }        
    return T_i10;
}
```

* `T_i11` represents the **maximum value of the negative** of all stock prices up to `i-th` day
  * Equivalently the **minimum** value of all the stock prices. [3, 4, 7, **2**, 6, 8, 12]

* `T_i11` represents the **decision** we should make: **sell** right now or **rest**

---



###### Case II: k = +Infinity

* If k is positive infinite, then there isn't really any difference between k and k - 1 (you can think of that as if n = 10 but k = 1000 and all the possible k would be from 1000 to 990 and will never be used up and make any difference)
* So it implies `T[i-1][k-1][0] = T[i-1][k][0]` and `T[i-1][k-1][1] = T[i-1][k][1]`. So the two variables`T[i][k][0]` and `T[i][k][1]` with `k = +Infinity`, and the recurrence relations say:

```java
T[i][k][0] = max(T[i-1][k][0], T[i-1][k][1] + prices[i])
T[i][k][1] = max(T[i-1][k][1], T[i-1][k-1][0] - prices[i]) 
					 = max(T[i-1][k][1], T[i-1][k][0] - prices[i])
```

where we have taken advantage of the fact that `T[i-1][k-1][0] = T[i-1][k][0]`

The `O(n)` time and `O(1)` space solution is as follows:

```java
public int maxProfit(int[] prices) {
    int T_ik0 = 0, T_ik1 = Integer.MIN_VALUE;
    
    for (int price : prices) {
        int T_ik0_old = T_ik0;
        T_ik0 = Math.max(T_ik0, T_ik1 + price);
        T_ik1 = Math.max(T_ik1, T_ik0_old - price);
    }
    
    return T_ik0;
}
```



###### Case III: k = 2

Similar to the case where `k = 1`, except now we have four variables instead of two on each day: `T[i][1][0]`, `T[i][1][1]`, `T[i][2][0]`, `T[i][2][1]`, and the recurrence relations are:

```java
T[i][2][0] = max(T[i-1][2][0], T[i-1][2][1] + prices[i])
T[i][2][1] = max(T[i-1][2][1], T[i-1][1][0] - prices[i])
T[i][1][0] = max(T[i-1][1][0], T[i-1][1][1] + prices[i])
T[i][1][1] = max(T[i-1][1][1], -prices[i]) // T[i][0][0] = 0
```

The `O(n)` time and `O(1)` space solution is as follows:

```java
public int maxProfit(int[] prices) {
    int T_i10 = 0, T_i11 = Integer.MIN_VALUE;
    int T_i20 = 0, T_i21 = Integer.MIN_VALUE;
        
    for (int price : prices) {
        T_i20 = Math.max(T_i20, T_i21 + price);
        T_i21 = Math.max(T_i21, T_i10 - price);
        T_i10 = Math.max(T_i10, T_i11 + price);
        T_i11 = Math.max(T_i11, -price);
    }
        
    return T_i20;
}
```



###### Case IV: k is arbitrary

* If `k >= n/2`, we can extend `k` to positive infinity and the problem is equivalent to **`Case II`**.
* If not, we should build an array for different ks

```java
public int maxProfit(int k, int[] prices) {
    if (k >= prices.length >>> 1) {
      	// case II
        int T_ik0 = 0, T_ik1 = Integer.MIN_VALUE;
    
        for (int price : prices) {
            int T_ik0_old = T_ik0;
            T_ik0 = Math.max(T_ik0, T_ik1 + price);
            T_ik1 = Math.max(T_ik1, T_ik0_old - price);
        }
        
        return T_ik0;
    }
        
    int[] T_ik0 = new int[k + 1];
    int[] T_ik1 = new int[k + 1];
    Arrays.fill(T_ik1, Integer.MIN_VALUE);
        
    for (int price : prices) {
        for (int j = k; j > 0; j--) {
            T_ik0[j] = Math.max(T_ik0[j], T_ik1[j] + price);
            T_ik1[j] = Math.max(T_ik1[j], T_ik0[j - 1] - price);
        }
    }
        
    return T_ik0[k];
}
```



###### Case V: `k = +Infinity but with cooldow`

With "cooldown", we cannot buy on the `i-th` day if a stock is sold on the `(i-1)-th` day. Therefore, in the second equation above, instead of `T[i-1][k][0]`, we should actually use `T[i-2][k][0]` if we intend to buy on the `i-th` day. 

```java
T[i][k][0] = max(T[i-1][k][0], T[i-1][k][1] + prices[i])
T[i][k][1] = max(T[i-1][k][1], T[i-2][k][0] - prices[i]) // difference here
```

Here is the `O(n)` time and `O(1)` space solution:

```java
public int maxProfit(int[] prices) {
    int T_ik0_pre = 0, T_ik0 = 0, T_ik1 = Integer.MIN_VALUE;
    
    for (int price : prices) {
        int T_ik0_old = T_ik0; // T_(i-2)k0
        T_ik0 = Math.max(T_ik0, T_ik1 + price);
        T_ik1 = Math.max(T_ik1, T_ik0_pre - price);
        T_ik0_pre = T_ik0_old;
    }
    
    return T_ik0;
}
```



###### Case VI: `k = +Infinity but with transaction fee`

```java
T[i][k][0] = max(T[i-1][k][0], T[i-1][k][1] + prices[i])
T[i][k][1] = max(T[i-1][k][1], T[i-1][k][0] - prices[i] - fee)

||

T[i][k][0] = max(T[i-1][k][0], T[i-1][k][1] + prices[i] - fee)
T[i][k][1] = max(T[i-1][k][1], T[i-1][k][0] - prices[i])
```



```java
public int maxProfit(int[] prices, int fee) {
    int T_ik0 = 0, T_ik1 = Integer.MIN_VALUE;
    
    for (int price : prices) {
        int T_ik0_old = T_ik0;
        T_ik0 = Math.max(T_ik0, T_ik1 + price);
        T_ik1 = Math.max(T_ik1, T_ik0_old - price - fee);
    }
        
    return T_ik0;
}
```

