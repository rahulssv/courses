# 2-D Dynamic Programming

### [Unique Paths](https://leetcode.com/problems/unique-paths/)

### **Recursion**

Check out the comments.

![https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/ljcsc.png](https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/ljcsc.png)

```java
// Define: opt(i, j) the number of ways to the point (i, j)
// (0, 0) is the starting point, (m - 1, n - 1) is the finish point
// Recurrence: opt(i, j) = opt(i - 1, j) + opt(i, j - 1)
// Init: opt(0, 0) = 1, opt(0, j) = opt(i, 0) = 1
public int uniquePaths(int m, int n) {
  if (m == 0 || n == 0) {
    throw new IllegalArgumentException("m or n can't be 0");
  }
  return numPaths(m - 1, n - 1);
}

private int numPaths(int i, int j) {
  if (i == 0 || j == 0) { // includes the row 0 and col 0
    return 1;
  }
  return numPaths(i - 1, j) + numPaths(i, j - 1);
}
```

**Time:** `O(2^{M + N})`

**Space:** `O(M + N)`

Recurrence Tree for complexity analysis:

![https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/8pax9.jpg](https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/8pax9.jpg)

### **DP (Top-down with Memoization)**

Use an 2D array `mem` to do memoization.

```java
public int uniquePaths(int m, int n) {
  if (m == 0 || n == 0) {
    throw new IllegalArgumentException("m or n can't be 0");
  }
  int[][] mem = new int[m][n];
  for (int i = 0; i < m; ++i) { // init
    for (int j = 0; j < n; ++j) {
      mem[i][j] = -1;
    }
  }
  return numPaths(m - 1, n - 1, mem);
}

private int numPaths(int i, int j, int[][] mem) {
  if (i == 0 || j == 0) {
    return 1;
  }
  if (mem[i - 1][j] == -1) mem[i - 1][j] = numPaths(i - 1, j, mem);
  if (mem[i][j - 1] == -1) mem[i][j - 1] = numPaths(i, j - 1, mem);
  return mem[i - 1][j] + mem[i][j - 1];
}
```

**Time:** `O(MN)` where `MN` is the number of subproblems.

**Space:** `O(MN)`

![https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/fbu40.jpg](https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/fbu40.jpg)

### **DP (Bottom-up)**

![https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/bckom.png](https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/bckom.png)

```java
public int uniquePaths(int m, int n) {
  if (m == 0 || n == 0) {
    throw new IllegalArgumentException("m or n can't be 0");
  }
  int[][] dp = new int[m][n];
  // init
  for (int i = 0; i < m; ++i) dp[i][0] = 1;
  for (int i = 0; i < n; ++i) dp[0][i] = 1;
  // dp
  for (int i = 1; i < m; ++i) {
    for (int j = 1; j < n; ++j) {
      dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
    }
  }
  return dp[m - 1][n - 1];
}
```

**Time:** `O(MN)`

**Space:** `O(MN)`

### **DP (Bottom-up, Linear Space)**

Reduce the O(MN)O(MN)*O*(*MN*) space complexity to O(N)O(N)*O*(*N*) (a row) or O(M)O(M)*O*(*M*) (a column). In terms of a row, we would update `dp[j]` by its old value plus `dp[j - 1]`.

![https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/2usv6.png](https://bloggg-1254259681.cos.na-siliconvalley.myqcloud.com/2usv6.png)

```java
public int uniquePaths(int m, int n) {
  if (m == 0 || n == 0) {
    throw new IllegalArgumentException("m or n can't be 0");
  }
  int[] dp = new int[n]; // row
  // init
  for (int i = 0; i < n; ++i) dp[i] = 1;
  // dp
  for (int i = 1; i < m; ++i) {
    for (int j = 1; j < n; ++j) {
      dp[j] = dp[j] + dp[j - 1];
    }
  }
  return dp[n - 1];
}
```

**Time:** `O(MN)`

**Space:** `O(N)` or `O(M)`

### [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

## **Brute Force**

```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        return longestCommonSubsequence(text1, text2, 0, 0);
    }
    
    private int longestCommonSubsequence(String text1, String text2, int i, int j) {
        if (i == text1.length() || j == text2.length())
            return 0;
        if (text1.charAt(i) == text2.charAt(j))
            return 1 + longestCommonSubsequence(text1, text2, i + 1, j + 1);
        else
            return Math.max(
                longestCommonSubsequence(text1, text2, i + 1, j),
                longestCommonSubsequence(text1, text2, i, j + 1)
            );
    }
}
```

## **Top-down DP**

We might use memoization to overcome overlapping subproblems.

Since there are two changing values, i.e. `i` and `j` in the recursive function `longestCommonSubsequence`, we might apply a two-dimensional array.

```java
class Solution {
    private Integer[][] dp;
    public int longestCommonSubsequence(String text1, String text2) {
        dp = new Integer[text1.length()][text2.length()];
        return longestCommonSubsequence(text1, text2, 0, 0);
    }
    
    private int longestCommonSubsequence(String text1, String text2, int i, int j) {
        if (i == text1.length() || j == text2.length())
            return 0;
        
        if (dp[i][j] != null)
            return dp[i][j];
            
        if (text1.charAt(i) == text2.charAt(j))
            return dp[i][j] = 1 + longestCommonSubsequence(text1, text2, i + 1, j + 1);
        else
            return dp[i][j] = Math.max(
                longestCommonSubsequence(text1, text2, i + 1, j),
                longestCommonSubsequence(text1, text2, i, j + 1)
            );
    }
}
```

## **Bottom-up DP**

For every `i` in text1, `j` in text2, we will choose one of the following two options:

- if two characters match, length of the common subsequence would be 1 plus the length of the common subsequence till the `i-1` and `j-1` indexes
- if two characters doesn't match, we will take the longer by either skipping `i` or `j` indexes

```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int[][] dp = new int[text1.length() + 1][text2.length() + 1];
        for (int i = 1; i <= text1.length(); i++) {
            for (int j = 1; j <= text2.length(); j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1))
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                else
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
        return dp[text1.length()][text2.length()];
    }
}
```

### [Best Time to Buy And Sell Stock With Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

The series of problems are typical dp. The key for dp is to find the variables to represent the states and deduce the transition function.

Of course one may come up with a O(1) space solution directly, but I think it is better to be generous when you think and be greedy when you implement.

The natural states for this problem is the 3 possible transactions : `buy`, `sell`, `rest`. Here `rest` means no transaction on that day (aka cooldown).

Then the transaction sequences can end with any of these three states.

For each of them we make an array, `buy[n]`, `sell[n]` and `rest[n]`.

`buy[i]` means before day `i` what is the maxProfit for any sequence end with `buy`.

`sell[i]` means before day `i` what is the maxProfit for any sequence end with `sell`.

`rest[i]` means before day `i` what is the maxProfit for any sequence end with `rest`.

Then we want to deduce the transition functions for `buy` `sell` and `rest`. By definition we have:

`buy[i]  = max(rest[i-1]-price, buy[i-1]) 
sell[i] = max(buy[i-1]+price, sell[i-1])
rest[i] = max(sell[i-1], buy[i-1], rest[i-1])`

Where `price` is the price of day `i`. All of these are very straightforward. They simply represents :

`(1) We have to `rest` before we `buy` and 
(2) we have to `buy` before we `sell``

One tricky point is how do you make sure you `sell` before you `buy`, since from the equations it seems that `[buy, rest, buy]` is entirely possible.

Well, the answer lies within the fact that `buy[i] <= rest[i]` which means `rest[i] = max(sell[i-1], rest[i-1])`. That made sure `[buy, rest, buy]` is never occurred.

A further observation is that and `rest[i] <= sell[i]` is also true therefore

`rest[i] = sell[i-1]`

Substitute this in to `buy[i]` we now have 2 functions instead of 3:

`buy[i] = max(sell[i-2]-price, buy[i-1])
sell[i] = max(buy[i-1]+price, sell[i-1])`

This is better than 3, but

**we can do even better**

Since states of day `i` relies only on `i-1` and `i-2` we can reduce the O(n) space to O(1). And here we are at our final solution:

**Java**

```java
public int maxProfit(int[] prices) {
    int sell = 0, prev_sell = 0, buy = Integer.MIN_VALUE, prev_buy;
    for (int price : prices) {
        prev_buy = buy;
        buy = Math.max(prev_sell - price, prev_buy);
        prev_sell = sell;
        sell = Math.max(prev_buy + price, prev_sell);
    }
    return sell;
}
```

### [Coin Change II](https://leetcode.com/problems/coin-change-ii/)

This is a classic knapsack problem. Honestly, I'm not good at knapsack problem, it's really tough for me.

`dp[i][j]` : the number of combinations to make up amount `j` by using the first `i` types of coins

`State transition`:

1. not using the `i`th coin, only using the first `i-1` coins to make up amount `j`, then we have `dp[i-1][j]` ways.
2. using the `i`th coin, since we can use unlimited same coin, we need to know how many ways to make up amount `j - coins[i-1]` by using first `i` coins(including `i`th), which is `dp[i][j-coins[i-1]]`

`Initialization`: `dp[i][0] = 1`

Once you figure out all these, it's easy to write out the code:

```java
    public int change(int amount, int[] coins) {
        int[][] dp = new int[coins.length+1][amount+1];
        dp[0][0] = 1;
        
        for (int i = 1; i <= coins.length; i++) {
            dp[i][0] = 1;
            for (int j = 1; j <= amount; j++) {
                dp[i][j] = dp[i-1][j] + (j >= coins[i-1] ? dp[i][j-coins[i-1]] : 0);
            }
        }
        return dp[coins.length][amount];
    }
```

Now we can see that `dp[i][j]` only rely on `dp[i-1][j]` and `dp[i][j-coins[i]]`, then we can optimize the space by only using one-dimension array.

```java
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i-coin];
            }
        }
        return dp[amount];
    }
```

### [Target Sum](https://leetcode.com/problems/target-sum/)

the THINKING process behind Dynamic Programming so that you can solve these questions on your own.

1. Category
    
    Most dynamic programming questions can be boiled down to a few categories. It's important to recognize the category because it allows us to FRAME a new question into something we already know. Frame means use the framework, not copy an approach from another problem into the current problem. You must understand that every DP problem is different.
    
    **Question:** Identify this problem as one of the categories below before continuing.
    
    - 0/1 Knapsack
    - Unbounded Knapsack
    - Shortest Path (eg: Unique Paths I/II)
    - Fibonacci Sequence (eg: House Thief, Jump Game)
    - Longest Common Substring/Subsequeunce
    
    **Answer:** 0/1 Knapsack
    
    *Why 0/1 Knapsack?* Our 'Capacity' is the target we want to reach 'S'. Our 'Items' are the numbers in the input subset and the 'Weights' of the items are the values of the numbers itself. This question follows 0/1 and not unbounded knapsack because we can use each number ONCE.
    
    *What is the variation?* The twist on this problem from standard knapsack is that we must add ALL items in the subset to our knapsack. We can reframe the question into adding the positive or negative value of the current number to our knapsack in order to reach the target capacity 'S'.
    
2. States
    
    What variables we need to keep track of in order to reach our optimal result? This Quora post explains state beautifully, so please refer to this link if you are confused: [www.quora.com/What-does-a-state-represent-in-terms-of-Dynamic-Programming](http://www.quora.com/What-does-a-state-represent-in-terms-of-Dynamic-Programming)
    
    **Question:** Determine State variables.
    
    *Hint:* As a general rule, Knapsack problems will require 2 states at minimum.
    
    **Answer:** Index and Current Sum
    
    *Why Index?* Index represents the index of the input subset we are considering. This tells us what values we have considered, what values we haven't considered, and what value we are currently considering. As a general rule, index is a required state in nearly all dynamic programming problems, except for shortest paths which is row and column instead of a single index but we'll get into that in a seperate post.
    
    *Why Current Sum?* The question asks us if we can sum every item (either the positive or negative value of that item) in the subset to reach the target value. Current Sum gives us the sum of all the values we have processed so far. Our answer revolves around Current Sum being equal to Target.
    
3. Decisions
    
    Dynamic Programming is all about making the optimal decision. In order to make the optimal decision, we will have to try all decisions first. The MIT lecture on DP (highly recommended) refers to this as the guessing step. My brain works better calling this a decision instead of a guess. Decisions will have to bring us closer to the base case and lead us towards the question we want to answer. Base case is covered in Step 4 but really work in tandem with the decision step.
    
    **Question:** What decisions do we have to make at each recursive call?
    
    *Hint:* As a general rule, Knapsack problems will require 2 decisions.
    
    **Answer:** This problem requires we take ALL items in our input subset, so at every step we will be adding an item to our knapsack. Remember, we stated in Step 2 that *"The question asks us if we can sum every item (either the positive or negative value of that item) in the subset to reach the target value."* The decision is:
    
    1. Should we add the current numbers positive value
    2. Should we add the current numbers negative value
    
    As a note, knapsack problems usually don't require us to take all items, thus a usual knapsack decision is to take the item or leave the item.
    
4. Base Case
    
    Base cases need to relate directly to the conditions required by the answer we are seeking. This is why it is important for our decisions to work towards our base cases, as it means our decisions are working towards our answer.
    
    Let's revisit the conditions for our answers.
    
    1. We use all numbers in our input subset.
    2. The sum of all numbers is equal to our target 'S'.
    
    **Question:** Identify the base cases.
    
    *Hint:* There are 2 base cases.
    
    **Answer:** We need 2 base cases. One for when the current state is valid and one for when the current state is invalid.
    
    1. Valid: Index is out of bounds AND current sum is equal to target 'S'
    2. Invalid: Index is out of bounds
    
    *Why Index is out of bounds?* A condition for our answer is that we use EVERY item in our input subset. When the index is out of bounds, we know we have considered every item in our input subset.
    
    *Why current sum is equal to target?* A condition for our answer is that the sum of using either the positive or negative values of items in our input subet equal to the target sum 'S'.
    
    If we have considered all the items in our input subset and our current sum is equal to our target, we have successfully met both conditions required by our answer.
    
    On the other hand, if we have considered all the items in our input subset and our current sum is NOT equal to our target, we have only met condition required by our answer. No bueno.
    
5. Code it
    
    If you've thought through all the steps and understand the problem, it's trivial to code the actual solution.
    
    ```python
     def findTargetSumWays(self, nums, S):
         index = len(nums) - 1
         curr_sum = 0
         return self.dp(nums, S, index, curr_sum)
         
     def dp(self, nums, target, index, curr_sum):
     	# Base Cases
         if index < 0 and curr_sum == target:
             return 1
         if index < 0:
             return 0 
         
     	# Decisions
         positive = self.dp(nums, target, index-1, curr_sum + nums[index])
         negative = self.dp(nums, target, index-1, curr_sum + -nums[index])
         
         return positive + negative
    ```
    
6. Optimize
    
    Once we introduce memoization, we will only solve each subproblem ONCE. We can remove recursion altogether and avoid the overhead and potential of a stack overflow by introducing tabulation. It's important to note that the top down recursive and bottom up tabulation methods perform the EXACT same amount of work. The only different is memory. If they peform the exact same amount of work, the conversion just requires us to specify the order in which problems should be solved. This post is really long now so I won't cover these steps here, possibly in a future post.
    

Memoization Solution for Reference

```python
class Solution:
    def findTargetSumWays(self, nums, S):
        index = len(nums) - 1
        curr_sum = 0
        self.memo = {}
        return self.dp(nums, S, index, curr_sum)
        
    def dp(self, nums, target, index, curr_sum):
        if (index, curr_sum) in self.memo:
            return self.memo[(index, curr_sum)]
        
        if index < 0 and curr_sum == target:
            return 1
        if index < 0:
            return 0 
        
        positive = self.dp(nums, target, index-1, curr_sum + nums[index])
        negative = self.dp(nums, target, index-1, curr_sum + -nums[index])
        
        self.memo[(index, curr_sum)] = positive + negative
        return self.memo[(index, curr_sum)]
```

Leave a comment on what DP problems you would like this type of post for next and upvote this solution if you found it helpful. I'd like to get this to the top because I'm honestly tired of seeing straight optimized tabulated solutions with no THINKING process behind it.

DP IS EASY!

```java
public class Solution {
    public int findTargetSumWays(int[] nums, int s) {
        int sum = 0; 
        for(int i: nums) sum+=i;
        if(s>sum || s<-sum) return 0;
        int[] dp = new int[2*sum+1];
        dp[0+sum] = 1;
        for(int i = 0; i<nums.length; i++){
            int[] next = new int[2*sum+1];
            for(int k = 0; k<2*sum+1; k++){
                if(dp[k]!=0){
                    next[k + nums[i]] += dp[k];
                    next[k - nums[i]] += dp[k];
                }
            }
            dp = next;
        }
        return dp[sum+s];
    }
}
```

![https://leetcode.com/uploads/files/1485048726667-screen-shot-2017-01-21-at-8.31.48-pm.jpg](https://leetcode.com/uploads/files/1485048726667-screen-shot-2017-01-21-at-8.31.48-pm.jpg)

### [Interleaving String](https://leetcode.com/problems/interleaving-string/)

## **BFS solution (6ms)**

Imagine a grid, which x-axis and y-axis are s1 and s2, matching s3 is the same as

finding a path from (0,0) to (len1, len2). It actually becomes a

BFS on grid. Since we don't need exact paths, a HashSet of

coordinates is used to eliminate duplicated paths.

```java
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int len1 = s1.length(),
            len2 = s2.length(),
            len3 = s3.length();
        if (len1 + len2 != len3) return false;
        Deque<Integer> queue = new LinkedList<>();
        int matched = 0;
        queue.offer(0);
        Set<Integer> set = new HashSet<>();
        while (queue.size() > 0 && matched < len3) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int p1 = queue.peek() / len3,
                    p2 = queue.peek() % len3;
                queue.poll();
                if (p1 < len1 && s1.charAt(p1) == s3.charAt(matched)) {
                    int key = (p1 + 1) * len3 + p2;
                    if (!set.contains(key)) {
                        set.add(key);
                        queue.offer(key);
                    }
                }
                if (p2 < len2 && s2.charAt(p2) == s3.charAt(matched)) {
                    int key = p1 * len3 + (p2 + 1);
                    if (!set.contains(key)) {
                        set.add(key);
                        queue.offer(key);
                    }
                }
            }
            matched++;
        }
        return queue.size() > 0 && matched == len3;
    }
}
```

## **DFS solution with memorization (2ms)**

This looks slow but is actually faster than BFS! Think about it carefully, in this

particular problem, search always ends at the same depth. DFS with memorization

searches about the same amount of paths with the same length as BFS, if it is doesn't

terminate on the first path found. Without the queue operations, the overall cost

is only smaller if we don't count call stack. The most significant runtime reducer is

probably the early termination

```java
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) return false;
        HashSet<Integer> cache = new HashSet<Integer>();
        return isInterleave0(s1, s2, s3, 0, 0, cache);
    }

    private boolean isInterleave0(String s1, String s2, String s3, int p1, int p2, HashSet<Integer> cache) {
        if (p1 + p2 == s3.length())
            return true;
        if (cache.contains(p1 * s3.length() + p2))
            return false;
        // no need to store actual result.
        // if we found the path, we have already terminated.
        cache.add(p1 * s3.length() + p2);
        boolean match1 = p1 < s1.length() && s3.charAt(p1 + p2) == s1.charAt(p1);
        boolean match2 = p2 < s2.length() && s3.charAt(p1 + p2) == s2.charAt(p2);
        if (match1 && match2)
            return isInterleave0(s1, s2, s3, p1 + 1, p2, cache) ||
                   isInterleave0(s1, s2, s3, p1, p2 + 1, cache);
        else if (match1)
            return isInterleave0(s1, s2, s3, p1 + 1, p2, cache);
        else if (match2)
            return isInterleave0(s1, s2, s3, p1, p2 + 1, cache);
        else
            return false;
    }
}
```

## **2d DP solution (6ms)**

It's an interesting practice. There are further optimization could be done to

reduce cache matrix to 1d. However doing DP for this problem is tedious and not

seem to worth the trouble.

```java
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int len1 = s1.length(),
            len2 = s2.length(),
            len3 = s3.length();
        if (len1 + len2 != len3) return false;
        // cache[i][j] == true means first i + j chars are matched by
        // first j chars from s1 and first i chars from s2
        boolean[][] cache = new boolean[len2 + 1][len1 + 1];
        cache[0][0] = true; // empty and empty matches empty
        int m3 = 1; // matched length, m1 and m2 are similar
        while (m3 <= len3) {
            // this loop fill in cache matrix from left-top to right-bottom, diagonally.
            // note that loop conditions are pretty tricky here.
            for (int m1 = Math.max(m3 - len2, 0); m1 <= len1 && m1 <= m3; m1++) {
                int m2 = m3 - m1;
                cache[m2][m1] =
                    m1 > 0 && cache[m2][m1 - 1] && s3.charAt(m3 - 1) == s1.charAt(m1 - 1) ||
                    m2 > 0 && cache[m2 - 1][m1] && s3.charAt(m3 - 1) == s2.charAt(m2 - 1);
            }
            m3++;
        }
        return cache[len2][len1];
    }
}
```

### [Longest Increasing Path In a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)

To get max length of increasing sequences:

1. Do `DFS` from every cell
2. Compare every 4 direction and skip cells that are out of boundary or smaller
3. Get matrix `max` from every cell's `max`
4. Use `matrix[x][y] <= matrix[i][j]` so we don't need a `visited[m][n]` array
5. The key is to `cache` the distance because it's highly possible to revisit a cell

Hope it helps!

```java
public static final int[][] dirs = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

public int longestIncreasingPath(int[][] matrix) {
    if(matrix.length == 0) return 0;
    int m = matrix.length, n = matrix[0].length;
    int[][] cache = new int[m][n];
    int max = 1;
    for(int i = 0; i < m; i++) {
        for(int j = 0; j < n; j++) {
            int len = dfs(matrix, i, j, m, n, cache);
            max = Math.max(max, len);
        }
    }   
    return max;
}

public int dfs(int[][] matrix, int i, int j, int m, int n, int[][] cache) {
    if(cache[i][j] != 0) return cache[i][j];
    int max = 1;
    for(int[] dir: dirs) {
        int x = i + dir[0], y = j + dir[1];
        if(x < 0 || x >= m || y < 0 || y >= n || matrix[x][y] <= matrix[i][j]) continue;
        int len = 1 + dfs(matrix, x, y, m, n, cache);
        max = Math.max(max, len);
    }
    cache[i][j] = max;
    return max;
}
```

### [Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

The idea is the following:

- we will build an array `mem` where `mem[i+1][j+1]` means that `S[0..j]` contains `T[0..i]` that many times as distinct subsequences. Therefor the result will be `mem[T.length()][S.length()]`.
- we can build this array rows-by-rows:
- the first row must be filled with 1. That's because the empty string is a subsequence of any string but only 1 time. So `mem[0][j] = 1` for every `j`. So with this we not only make our lives easier, but we also return correct value if `T` is an empty string.
- the first column of every rows except the first must be 0. This is because an empty string cannot contain a non-empty string as a substring -- the very first item of the array: `mem[0][0] = 1`, because an empty string contains the empty string 1 time.

So the matrix looks like this:

  `S 0123....j
T +----------+
  |1111111111|
0 |0         |
1 |0         |
2 |0         |
. |0         |
. |0         |
i |0         |`

From here we can easily fill the whole grid: for each `(x, y)`, we check if `S[x] == T[y]` we add the previous item and the previous item in the previous row, otherwise we copy the previous item in the same row. The reason is simple:

- if the current character in S doesn't equal to current character T, then we have the same number of distinct subsequences as we had without the new character.
- if the current character in S equal to the current character T, then the distinct number of subsequences: the number we had before **plus** the distinct number of subsequences we had with less longer T and less longer S.

An example:

`S: [acdabefbc]` and `T: [ab]`

first we check with `a`:

           `*  *
      S = [acdabefbc]
mem[1] = [0111222222]`

then we check with `ab`:

               `*  * ]
      S = [acdabefbc]
mem[1] = [0111222222]
mem[2] = [0000022244]`

And the result is 4, as the distinct subsequences are:

      `S = [a   b    ]
      S = [a      b ]
      S = [   ab    ]
      S = [   a   b ]`

See the code in Java:

```java
public int numDistinct(String S, String T) {
    // array creation
    int[][] mem = new int[T.length()+1][S.length()+1];

    // filling the first row: with 1s
    for(int j=0; j<=S.length(); j++) {
        mem[0][j] = 1;
    }
    
    // the first column is 0 by default in every other rows but the first, which we need.
    
    for(int i=0; i<T.length(); i++) {
        for(int j=0; j<S.length(); j++) {
            if(T.charAt(i) == S.charAt(j)) {
                mem[i+1][j+1] = mem[i][j] + mem[i+1][j];
            } else {
                mem[i+1][j+1] = mem[i+1][j];
            }
        }
    }
    
    return mem[T.length()][S.length()];
}
```

### [Edit Distance](https://leetcode.com/problems/edit-distance/)

First we may want to consider recursion.

```java
public class Solution {
    /**
     * Recursive solution.
     * For each poisition, check three subproblem:
     * 1. insert
     * 2. delete
     * 3. replace
     * We only modify the first string since no matter which one we choose, the result is the same. 
     * Got TLE since we recursively solve the same subproblem several times.
     * Appromixately O(len1 ^ 3) time in the worst case.
     * Need to optimize it using cache, which is the idea of dynamic programming. 
     * The key point is to find out the subproblem we have solved duplicately and cache the recursion.
     * Noticed that each subproblem is specificed by i and j pointer, so we can cache the result of these subproblems. 
     */
    public int minDistance(String word1, String word2) {
        if (word1 == null || word1.length() == 0) return word2.length();
        if (word2 == null || word2.length() == 0) return word1.length();
        
        return match(word1, word2, 0, 0);
    }
    
    private int match(String s1, String s2, int i, int j) {
        //If one of the string's pointer have reached the end of it
        if (s1.length() == i) {
            return s2.length() - j;
        }
        if (s2.length() == j) {
            return s1.length() - i;
        }
        
        int res;
        //If current poisition is the same.
        if (s1.charAt(i) == s2.charAt(j)) {
            res = match(s1, s2, i + 1, j + 1);
        } else {
            //Case1: insert
            int insert = match(s1, s2, i, j + 1);
            //Case2: delete
            int delete = match(s1, s2, i + 1, j);
            //Case3: replace
            int replace = match(s1, s2, i + 1, j + 1);
            res = Math.min(Math.min(insert, delete), replace) + 1;
        }
        
        return res;
    }
}
```

This got TLE. based on the analysis above, we may try DP.

```java
public class Solution {
    /**
     * Optimization using dynamic programming
     * Top-down solution
     * O(len1 * len2) time, O(len1 * len2) space
     */
    public int minDistance(String word1, String word2) {
        if (word1 == null || word2 == null) return -1;
        if (word1.length() == 0) return word2.length();
        if (word2.length() == 0) return word1.length();
        
        char[] c1 = word1.toCharArray();
        char[] c2 = word2.toCharArray();
        
        int[][] cache = new int[c1.length][c2.length];
        for (int i = 0; i < c1.length; i++) {
            for (int j = 0; j < c2.length; j++) {
                cache[i][j] = -1;
            }
        }
        
        return match(c1, c2, 0, 0, cache);
    }
    
    private int match(char[] c1, char[] c2, int i, int j, int[][] cache) {
        if (c1.length == i) return c2.length - j;
        if (c2.length == j) return c1.length - i;
        
        if (cache[i][j] != -1) {
            return cache[i][j];
        }
        
        if (c1[i] == c2[j]) {
            cache[i][j] = match(c1, c2, i + 1, j + 1, cache);
        } else {
            //Case1: insert
            int insert = match(c1, c2, i, j + 1, cache);
            //Case2: delete
            int delete = match(c1, c2, i + 1, j, cache);
            //Case3: replace
            int replace = match(c1, c2, i + 1, j + 1, cache);
            
            cache[i][j] = Math.min(Math.min(insert, delete), replace) + 1;
        }
        
        return cache[i][j];
    }
    
    
    
    
    /**
     * Bottom-up approach
     */
    public int minDistance(String word1, String word2) {
        if (word1 == null || word2 == null) return -1;
        if (word1.length() == 0) return word2.length();
        if (word2.length() == 0) return word1.length();
        
        char[] c1 = word1.toCharArray();
        char[] c2 = word2.toCharArray();
        
        int[][] matched = new int[c1.length + 1][c2.length + 1];
        //matched[length of c1 already been matched][length of c2 already been matched]
        
        for (int i = 0; i <= c1.length; i++) {
            matched[i][0] = i;
        }
        for (int j = 0; j <= c2.length; j++) {
            matched[0][j] = j;
        }
        
        for (int i = 0; i < c1.length; i++) {
            for (int j = 0; j < c2.length; j++) {
                if (c1[i] == c2[j]) {
                    matched[i + 1][j + 1] = matched[i][j];
                } else {
                    matched[i + 1][j + 1] = Math.min(Math.min(matched[i][j + 1], matched[i + 1][j]), matched[i][j]) + 1;
                    //Since it is bottom up, we are considering in the ascending order of indexes.
                    //Insert means plus 1 to j, delete means plus 1 to i, replace means plus 1 to both i and j. 
                    //above sequence is delete, insert and replace. 
                }
            }
        }
        
        return matched[c1.length][c2.length];
    }
    
}
```

### [Burst Balloons](https://leetcode.com/problems/burst-balloons/)

**Be Naive First**

When I first get this problem, it is far from dynamic programming to me. I started with the most naive idea the backtracking.

We have n balloons to burst, which mean we have n steps in the game. In the i th step we have n-i balloons to burst, i = 0~n-1. Therefore we are looking at an algorithm of O(n!). Well, it is slow, probably works for n < 12 only.

Of course this is not the point to implement it. We need to identify the redundant works we did in it and try to optimize.

Well, we can find that for any balloons left the maxCoins does not depends on the balloons already bursted. This indicate that we can use memorization (top down) or dynamic programming (bottom up) for all the cases from small numbers of balloon until n balloons. How many cases are there? For k balloons there are C(n, k) cases and for each case it need to scan the k balloons to compare. The sum is quite big still. It is better than O(n!) but worse than O(2^n).

**Better idea**

We then think can we apply the divide and conquer technique? After all there seems to be many self similar sub problems from the previous analysis.

Well, the nature way to divide the problem is burst one balloon and separate the balloons into 2 sub sections one on the left and one one the right. However, in this problem the left and right become adjacent and have effects on the maxCoins in the future.

Then another interesting idea come up. Which is quite often seen in dp problem analysis. That is reverse thinking. Like I said the coins you get for a balloon does not depend on the balloons already burst. Therefore

instead of divide the problem by the first balloon to burst, we divide the problem by the last balloon to burst.

Why is that? Because only the first and last balloons we are sure of their adjacent balloons before hand!

For the first we have `nums[i-1]*nums[i]*nums[i+1]` for the last we have `nums[-1]*nums[i]*nums[n]`.

OK. Think about n balloons if i is the last one to burst, what now?

We can see that the balloons is again separated into 2 sections. But this time since the balloon i is the last balloon of all to burst, the left and right section now has well defined boundary and do not affect each other! Therefore we can do either recursive method with memoization or dp.

**Final**

Here comes the final solutions. Note that we put 2 balloons with 1 as boundaries and also burst all the zero balloons in the first round since they won't give any coins.

The algorithm runs in O(n^3) which can be easily seen from the 3 loops in dp solution.

**Java D&C with Memoization**

```java
public int maxCoins(int[] iNums) {
    int[] nums = new int[iNums.length + 2];
    int n = 1;
    for (int x : iNums) if (x > 0) nums[n++] = x;
    nums[0] = nums[n++] = 1;

    int[][] memo = new int[n][n];
    return burst(memo, nums, 0, n - 1);
}

public int burst(int[][] memo, int[] nums, int left, int right) {
    if (left + 1 == right) return 0;
    if (memo[left][right] > 0) return memo[left][right];
    int ans = 0;
    for (int i = left + 1; i < right; ++i)
        ans = Math.max(ans, nums[left] * nums[i] * nums[right] 
        + burst(memo, nums, left, i) + burst(memo, nums, i, right));
    memo[left][right] = ans;
    return ans;
}
// 12 ms
```

**Java DP**

```java
public int maxCoins(int[] iNums) {
    int[] nums = new int[iNums.length + 2];
    int n = 1;
    for (int x : iNums) if (x > 0) nums[n++] = x;
    nums[0] = nums[n++] = 1;

    int[][] dp = new int[n][n];
    for (int k = 2; k < n; ++k)
        for (int left = 0; left < n - k; ++left) {
            int right = left + k;
            for (int i = left + 1; i < right; ++i)
                dp[left][right] = Math.max(dp[left][right], 
                nums[left] * nums[i] * nums[right] + dp[left][i] + dp[i][right]);
        }

    return dp[0][n - 1];
}
// 17 ms
```

### [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

This Solution use 2D DP. beat 90% solutions, very simple.

Here are some conditions to figure out, then the logic can be very straightforward.

```java
1, If p.charAt(j) == s.charAt(i) :  dp[i][j] = dp[i-1][j-1];
2, If p.charAt(j) == '.' : dp[i][j] = dp[i-1][j-1];
3, If p.charAt(j) == '*': 
   here are two sub conditions:
               1   if p.charAt(j-1) != s.charAt(i) : dp[i][j] = dp[i][j-2]  //in this case, a* only counts as empty
               2   if p.charAt(i-1) == s.charAt(i) or p.charAt(i-1) == '.':
                              dp[i][j] = dp[i-1][j]    //in this case, a* counts as multiple a 
                           or dp[i][j] = dp[i][j-1]   // in this case, a* counts as single a
                           or dp[i][j] = dp[i][j-2]   // in this case, a* counts as empty
```

Here is the solution

```java
public boolean isMatch(String s, String p) {

    if (s == null || p == null) {
        return false;
    }
    boolean[][] dp = new boolean[s.length()+1][p.length()+1];
    dp[0][0] = true;
    for (int i = 0; i < p.length(); i++) {
        if (p.charAt(i) == '*' && dp[0][i-1]) {
            dp[0][i+1] = true;
        }
    }
    for (int i = 0 ; i < s.length(); i++) {
        for (int j = 0; j < p.length(); j++) {
            if (p.charAt(j) == '.') {
                dp[i+1][j+1] = dp[i][j];
            }
            if (p.charAt(j) == s.charAt(i)) {
                dp[i+1][j+1] = dp[i][j];
            }
            if (p.charAt(j) == '*') {
                if (p.charAt(j-1) != s.charAt(i) && p.charAt(j-1) != '.') {
                    dp[i+1][j+1] = dp[i+1][j-1];
                } else {
                    dp[i+1][j+1] = (dp[i+1][j] || dp[i][j+1] || dp[i+1][j-1]);
                }
            }
        }
    }
    return dp[s.length()][p.length()];
}
```