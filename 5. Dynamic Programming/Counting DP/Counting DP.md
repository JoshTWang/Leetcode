* One type of DP ask for either the **maximum**, **minimum**, or **longest** of something.

* Another type of DP ask for the number of **distinct ways** to do something, another term used to describe this class of problems is **counting DP**

##### Differences with maximum or counting

###### maximum/minimum

* The recurrence relation typically involves a max() or min() function.
* If the state goes out of bounds, the base case equals to 0.

###### Counting

* With counting DP, dp(i) = dp(i - 1) + dp(i - 2). There is no max() or min().
* The base cases are often not set to 0. This is because the recurrence relation usually only involves addition terms with other states, so if the base case was set to \text{0}0 then you would only ever add \text{0}0 to itself.