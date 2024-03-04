# 13. 1-D Dynamic Programming

### [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

Recursion

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }
        return climbStairs(n-1) + climbStairs(n-2);
    }
}
```

Memoization

```java
class Solution {
    public int climbStairs(int n) {
        Map<Integer, Integer> memo = new HashMap<>();
        return climbStairs(n, memo);
    }
    
    private int climbStairs(int n, Map<Integer, Integer> memo) {
        if (n == 0 || n == 1) {
            return 1;
        }
        if (!memo.containsKey(n)) {
            memo.put(n, climbStairs(n-1, memo) + climbStairs(n-2, memo));
        }
        return memo.get(n);
    }
}
```

Tabulation 

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }

        int[] dp = new int[n+1];
        dp[0] = dp[1] = 1;
        
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```

Space Optimization

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }
        int prev = 1, curr = 1;
        for (int i = 2; i <= n; i++) {
            int temp = curr;
            curr = prev + curr;
            prev = temp;
        }
        return curr;
    }
}
```

### [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)

We start at either step 0 or step 1. The target is to reach either last or second last step, whichever is minimum.

**Step 1 - Identify a recurrence relation between subproblems.** In this problem,

Recurrence Relation:

`mincost(i) = cost[i]+min(mincost(i-1), mincost(i-2))`

Base cases:

`mincost(0) = cost[0]`

`mincost(1) = cost[1]`

**Step 2 - Convert the recurrence relation to recursion**

```java
// Recursive Top Down - O(2^n) Time Limit Exceeded
public int minCostClimbingStairs(int[] cost) {
	int n = cost.length;
	return Math.min(minCost(cost, n-1), minCost(cost, n-2));
}
private int minCost(int[] cost, int n) {
	if (n < 0) return 0;
	if (n==0 || n==1) return cost[n];
	return cost[n] + Math.min(minCost(cost, n-1), minCost(cost, n-2));
}
```

**Step 3 - Optimization 1 - Top Down DP - Add memoization to recursion** - From exponential to linear.

```java
`// Top Down Memoization - O(n) 1ms
int[] dp;
public int minCostClimbingStairs(int[] cost) {
	int n = cost.length;
	dp = new int[n];
	return Math.min(minCost(cost, n-1), minCost(cost, n-2));
}
private int minCost(int[] cost, int n) {
	if (n < 0) return 0;
	if (n==0 || n==1) return cost[n];
	if (dp[n] != 0) return dp[n];
	dp[n] = cost[n] + Math.min(minCost(cost, n-1), minCost(cost, n-2));
	return dp[n];
}`
```

**Step 4 - Optimization 2 -Bottom Up DP - Convert recursion to iteration** - Getting rid of recursive stack

```java
// Bottom up tabulation - O(n) 1ms
public int minCostClimbingStairs(int[] cost) {
	int n = cost.length;
	int[] dp = new int[n];
	for (int i=0; i<n; i++) {
		if (i<2) dp[i] = cost[i];
		else dp[i] = cost[i] + Math.min(dp[i-1], dp[i-2]);
	}
	return Math.min(dp[n-1], dp[n-2]);
}
```

**Step 5 - Optimization 3 - Fine Tuning - Reduce O(n) space to O(1)**.

```java
// Bottom up computation - O(n) time, O(1) space
public int minCostClimbingStairs(int[] cost) {
	int n = cost.length;
	int first = cost[0];
	int second = cost[1];
	if (n<=2) return Math.min(first, second);
	for (int i=2; i<n; i++) {
		int curr = cost[i] + Math.min(first, second);
		first = second;
		second = curr;
	}
	return Math.min(first, second);
}
```

### [House Robber](https://leetcode.com/problems/house-robber/)

1. Find recursive relation
2. Recursive (top-down)
3. Recursive + memo (top-down)
4. Iterative + memo (bottom-up)
5. Iterative + N variables (bottom-up)

**Step 1.** Figure out recursive relation.

A robber has 2 options: a) rob current house `i`; b) don't rob current house.

If an option "a" is selected it means she can't rob previous `i-1` house but can safely proceed to the one before previous `i-2` and gets all cumulative loot that follows.

If an option "b" is selected the robber gets all the possible loot from robbery of `i-1` and all the following buildings.

So it boils down to calculating what is more profitable:

- robbery of current house + loot from houses before the previous
- loot from the previous house robbery and any loot captured before that

`rob(i) = Math.max( rob(i - 2) + currentHouseValue, rob(i - 1) )`

**Step 2.** Recursive (top-down)

Converting the recurrent relation from Step 1 shound't be very hard.

```java
public int rob(int[] nums) {
    return rob(nums, nums.length - 1);
}
private int rob(int[] nums, int i) {
    if (i < 0) {
        return 0;
    }
    return Math.max(rob(nums, i - 2) + nums[i], rob(nums, i - 1));
}
```

This algorithm will process the same `i` multiple times and it needs improvement. Time complexity: [to fill]

**Step 3.** Recursive + memo (top-down).

```java
int[] memo;
public int rob(int[] nums) {
    memo = new int[nums.length + 1];
    Arrays.fill(memo, -1);
    return rob(nums, nums.length - 1);
}

private int rob(int[] nums, int i) {
    if (i < 0) {
        return 0;
    }
    if (memo[i] >= 0) {
        return memo[i];
    }
    int result = Math.max(rob(nums, i - 2) + nums[i], rob(nums, i - 1));
    memo[i] = result;
    return result;
}
```

Much better, this should run in `O(n)` time. Space complexity is `O(n)` as well, because of the recursion stack, let's try to get rid of it.

**Step 4.** Iterative + memo (bottom-up)

```java
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    int[] memo = new int[nums.length + 1];
    memo[0] = 0;
    memo[1] = nums[0];
    for (int i = 1; i < nums.length; i++) {
        int val = nums[i];
        memo[i+1] = Math.max(memo[i], memo[i-1] + val);
    }
    return memo[nums.length];
}
```

**Step 5.** Iterative + 2 variables (bottom-up)

We can notice that in the previous step we use only `memo[i]` and `memo[i-1]`, so going just 2 steps back. We can hold them in 2 variables instead. This optimization is met in Fibonacci sequence creation and some other problems [to paste links].

```java
/* the order is: prev2, prev1, num  */
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    int prev1 = 0;
    int prev2 = 0;
    for (int num : nums) {
        int tmp = prev1;
        prev1 = Math.max(prev2 + num, prev1);
        prev2 = tmp;
    }
    return prev1;
}
```

### [House Robber II](https://leetcode.com/problems/house-robber-ii/)

Since this question is a follow-up to House Robber, we can assume we already have a way to solve the simpler question, i.e. given a 1 row of house, we know how to rob them. So we already have such a helper function. We modify it a bit to rob a given range of houses.

```java
private int rob(int[] num, int lo, int hi) {
    int include = 0, exclude = 0;
    for (int j = lo; j <= hi; j++) {
        int i = include, e = exclude;
        include = e + num[j];
        exclude = Math.max(e, i);
    }
    return Math.max(include, exclude);
}
```

Now the question is how to rob a circular row of houses. It is a bit complicated to solve like the simpler question. It is because in the simpler question whether to rob *num[lo]* is entirely our choice. But, it is now constrained by whether *num[hi]* is robbed.

However, since we already have a nice solution to the simpler problem. We do not want to throw it away. Then, it becomes how can we reduce this problem to the simpler one. Actually, extending from the logic that if house i is not robbed, then you are free to choose whether to rob house i + 1, you can break the circle by assuming a house is not robbed.

For example, 1 -> 2 -> 3 -> 1 becomes 2 -> 3 if 1 is not robbed.

Since every house is either robbed or not robbed and at least half of the houses are not robbed, the solution is simply the larger of two cases with consecutive houses, i.e. house i not robbed, break the circle, solve it, or house i + 1 not robbed. Hence, the following solution. I chose i = n and i + 1 = 0 for simpler coding. But, you can choose whichever two consecutive ones.

```java
public int rob(int[] nums) {
    if (nums.length == 1) return nums[0];
    return Math.max(rob(nums, 0, nums.length - 2), rob(nums, 1, nums.length - 1));
}
```

### [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

`dp(i, j)` represents whether `s(i ... j)` can form a palindromic substring, `dp(i, j)` is true when `s(i)` equals to `s(j)` and `s(i+1 ... j-1)` is a palindromic substring. When we found a palindrome, check if it's the longest one. Time complexity O(n^2).

```java
public String longestPalindrome(String s) {
  int n = s.length();
  String res = null;
    
  boolean[][] dp = new boolean[n][n];
    
  for (int i = n - 1; i >= 0; i--) {
    for (int j = i; j < n; j++) {
      dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i < 3 || dp[i + 1][j - 1]);
            
      if (dp[i][j] && (res == null || j - i + 1 > res.length())) {
        res = s.substring(i, j + 1);
      }
    }
  }
    
  return res;
}
```

### [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)

**Step 1:** Start a for loop to point at every single character from where we will trace the palindrome string.

checkPalindrome(s,i,i); //To check the palindrome of odd length palindromic sub-string

checkPalindrome(s,i,i+1); //To check the palindrome of even length palindromic sub-string

**Step 2:** From each character of the string, we will keep checking if the sub-string is a palindrome and increment the palindrome count. To check the palindrome, keep checking the left and right of the character if it is same or not.

**First Loop:**

![https://discuss.leetcode.com/assets/uploads/files/1500788789821-300147d3-e98e-4977-83f1-9eb8213a485e-image.png](https://discuss.leetcode.com/assets/uploads/files/1500788789821-300147d3-e98e-4977-83f1-9eb8213a485e-image.png)

Palindrome: a (Count=1)

![https://discuss.leetcode.com/assets/uploads/files/1500788808273-fec1dec5-ab5f-44cf-8dbd-eb2780e8d65f-image.png](https://discuss.leetcode.com/assets/uploads/files/1500788808273-fec1dec5-ab5f-44cf-8dbd-eb2780e8d65f-image.png)

Palindrome: aa (Count=2)

**Second Loop:**

![https://discuss.leetcode.com/assets/uploads/files/1500788845825-881440b8-6dde-4b6f-a864-24fef277069b-image.png](https://discuss.leetcode.com/assets/uploads/files/1500788845825-881440b8-6dde-4b6f-a864-24fef277069b-image.png)

Palindrome: a (Count=3)

![https://discuss.leetcode.com/assets/uploads/files/1500788872992-61fc20cb-0cb2-4179-8f5a-529cbad7a2ec-image.png](https://discuss.leetcode.com/assets/uploads/files/1500788872992-61fc20cb-0cb2-4179-8f5a-529cbad7a2ec-image.png)

Palindrome: No Palindrome

**Third Loop:**

![https://discuss.leetcode.com/assets/uploads/files/1500788901208-bf12b13b-ff32-4703-86cf-0bcb54465428-image.png](https://discuss.leetcode.com/assets/uploads/files/1500788901208-bf12b13b-ff32-4703-86cf-0bcb54465428-image.png)

Palindrome: b,aba,aabaa (Count=6)

![https://discuss.leetcode.com/assets/uploads/files/1500788934464-5cc2c31d-404c-456a-a77d-1432bb0c679b-image.png](https://discuss.leetcode.com/assets/uploads/files/1500788934464-5cc2c31d-404c-456a-a77d-1432bb0c679b-image.png)

Palindrome: No Palindrome

**Forth Loop:**

![https://discuss.leetcode.com/assets/uploads/files/1500788981974-a2d3f30e-0745-4a75-b2c0-940834bd6a84-image.png](https://discuss.leetcode.com/assets/uploads/files/1500788981974-a2d3f30e-0745-4a75-b2c0-940834bd6a84-image.png)

Palindrome: a (Count=7)

![https://discuss.leetcode.com/assets/uploads/files/1500789009507-f38aa5c2-17ac-47db-8fe9-b9bb4ceb1407-image.png](https://discuss.leetcode.com/assets/uploads/files/1500789009507-f38aa5c2-17ac-47db-8fe9-b9bb4ceb1407-image.png)

Palindrome: aa (Count=8)

Count = 9 (For the last character)

**Answer = 9**

'''

```java
int count =1;
public int countSubstrings(String s) {
    if(s.length()==0) 
        return 0;
    for(int i=0; i<s.length()-1; i++){
        checkPalindrome(s,i,i);     //To check the palindrome of odd length palindromic sub-string
        checkPalindrome(s,i,i+1);   //To check the palindrome of even length palindromic sub-string
    }
    return count;
}    

private void checkPalindrome(String s, int i, int j) {
    while(i>=0 && j<s.length() && s.charAt(i)==s.charAt(j)){    //Check for the palindrome string 
        count++;    //Increment the count if palindromin substring found
        i--;    //To trace string in left direction
        j++;    //To trace string in right direction
    }
}
```

### [Decode Ways](https://leetcode.com/problems/decode-ways/)

I used a dp array of size n + 1 to save subproblem solutions. `dp[0]` means an empty string will have one way to decode, `dp[1]` means the way to decode a string of size 1. I then check one digit and two digit combination and save the results along the way. In the end, `dp[n]` will be the end result.

```java
public class Solution {
    public int numDecodings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        int n = s.length();
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = s.charAt(0) != '0' ? 1 : 0;
        for (int i = 2; i <= n; i++) {
            int first = Integer.valueOf(s.substring(i - 1, i));
            int second = Integer.valueOf(s.substring(i - 2, i));
            if (first >= 1 && first <= 9) {
               dp[i] += dp[i-1];  
            }
            if (second >= 10 && second <= 26) {
                dp[i] += dp[i-2];
            }
        }
        return dp[n];
    }
}
```

### [Coin Change](https://leetcode.com/problems/coin-change/)

Recursive Method:

The idea is very classic dynamic programming: think of the last step we take. Suppose we have already found out the best way to sum up to amount `a`, then for the last step, we can choose any coin type which gives us a remainder `r` where `r = a-coins[i]` for all `i`'s. For every remainder, go through exactly the same process as before until either the remainder is 0 or less than 0 (meaning not a valid solution). With this idea, the only remaining detail is to store the minimum number of coins needed to sum up to `r` so that we don't need to recompute it over and over again.

Code in Java:

```java
public class Solution {
public int coinChange(int[] coins, int amount) {
    if(amount<1) return 0;
    return helper(coins, amount, new int[amount]);
}

private int helper(int[] coins, int rem, int[] count) { // rem: remaining coins after the last step; count[rem]: minimum number of coins to sum up to rem
    if(rem<0) return -1; // not valid
    if(rem==0) return 0; // completed
    if(count[rem-1] != 0) return count[rem-1]; // already computed, so reuse
    int min = Integer.MAX_VALUE;
    for(int coin : coins) {
        int res = helper(coins, rem-coin, count);
        if(res>=0 && res < min)
            min = 1+res;
    }
    count[rem-1] = (min==Integer.MAX_VALUE) ? -1 : min;
    return count[rem-1];
}
}
```

Iterative Method:

For the iterative solution, we think in bottom-up manner. Suppose we have already computed all the minimum counts up to `sum`, what would be the minimum count for `sum+1`?

Code in Java:

```java
public class Solution {
public int coinChange(int[] coins, int amount) {
    if(amount<1) return 0;
    int[] dp = new int[amount+1];
    int sum = 0;
    
	while(++sum<=amount) {
		int min = -1;
    	for(int coin : coins) {
    		if(sum >= coin && dp[sum-coin]!=-1) {
    			int temp = dp[sum-coin]+1;
    			min = min<0 ? temp : (temp < min ? temp : min);
    		}
    	}
    	dp[sum] = min;
	}
	return dp[amount];
}
}
```

### [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

**Intution:** Since we have to find the contiguous subarray having maximum product then your approach should be combination of following three cases :

- **Case1 :- All the elements are positive :** Then your answer will be product of all the elements in the array.
- **Case2 :- Array have positive and negative elements both :**
    1. If the number of negative elements is even then again your answer will be complete array because on multiplying all the negative numbers it will become positive.
    2. If the number of negative elements is odd then you have to remove just one negative element and for that u need to check your subarrays to get the max product.
- **Case3 :- Array also contains 0 :** Then there will be not much difference...its just that your array will be divided into subarray around that 0. What u have to so is just as soon as your product becomes 0 make it 1 for the next iteration, now u will be searching new subarray and previous max will already be updated.(These cases are much clear in approach 3)
- * As it is said "Talk is Cheap, Show me the Code", so based on above discussion we can frame our code in many different ways, out of which I have mentioned 3 intutive approaches.

**Approach 1:** For each index i keep updating the max and min. We are also keeping min because on multiplying with any negative number your min will become max and max will become min. So for every index i we will take max of (i-th element, prevMax * i-th element, prevMin * i-th element).

```java
class Solution {
    public int maxProduct(int[] nums) {
        
        int max = nums[0], min = nums[0], ans = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            
            int temp = max;  // store the max because before updating min your max will already be updated
            
            max = Math.max(Math.max(max * nums[i], min * nums[i]), nums[i]);
            min = Math.min(Math.min(temp * nums[i], min * nums[i]), nums[i]);
            
            if (max > ans) {
                ans = max;
            }
        }
        
        return ans;

    }
}
```

**Approach 2:** Just the slight modification of previous approach. As we know that on multiplying with negative number max will become min and min will become max, so why not as soon as we encounter negative element, we swap the max and min already.

```java
class Solution {
    public int maxProduct(int[] nums) {
        
        int max = nums[0], min = nums[0], ans = nums[0];
        int n = nums.length;
        
        for (int i = 1; i < n; i++) {
        
			// Swapping min and max
            if (nums[i] < 0){
                int temp = max;
                max = min;
                min = temp;
            }
                

            max = Math.max(nums[i], max * nums[i]);
            min = Math.min(nums[i], min * nums[i]);

            ans = Math.max(ans, max);
        }
        
        return ans;

    }
}
```

**Approach 3:** Two pointer Approach

Explanation :

1.) Through intution explanation we know that if all the elements are positive or the negative elements are even then ur answer will be product of complete array which u will get in variable l and r at the last iteration.

2.) But if negative elements are odd then u have to remove one negative element and it is sure that it will be either right of max prefix product or left of max suffix product. So u need not to modify anything in your code as u are getting prefix product in l and suffix prduxt in r.

3.) If array also contains 0 then your l and r will become 0 at that point...then just update it to 1(or else u will keep multiplying with 0) to get the product ahead making another subarray.

![https://assets.leetcode.com/users/images/2ce0da10-9355-4018-a256-cba3a41af56d_1638500369.5001783.jpeg](https://assets.leetcode.com/users/images/2ce0da10-9355-4018-a256-cba3a41af56d_1638500369.5001783.jpeg)

```java
class Solution {
    public int maxProduct(int[] nums) {
        
        int n = nums.length;
        int l=1,r=1;
        int ans=nums[0];
        
        for(int i=0;i<n;i++){
            
			//if any of l or r become 0 then update it to 1
            l = l==0 ? 1 : l;
            r = r==0 ? 1 : r;
            
            l *= nums[i];   //prefix product
            r *= nums[n-1-i];    //suffix product
            
            ans = Math.max(ans,Math.max(l,r));
            
        }
        
        return ans;

    }
}
```

### [Word Break](https://leetcode.com/problems/word-break/)

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        // put all words into a hashset
        Set<String> set = new HashSet<>(wordDict);
        return wb(s, set);
    }
    private boolean wb(String s, Set<String> set) {
        int len = s.length();
        if (len == 0) {
            return true;
        }
        for (int i = 1; i <= len; ++i) {
            if (set.contains(s.substring(0, i)) && wb(s.substring(i), set)) {
                return true;
            }
        }
        return false;
    }
}
```

The time complexity depends on how many nodes the recursion tree has. In the worst case, the recursion tree has the most nodes, which means the program should not return in the middle and it should try as many possibilities as possible. So the branches and depth of the tree are as many as possible. For the worst case, for example, we take `s = "abcd"` and `wordDict = ["a", "b", "c", "bc", "ab", "abc"]`, the recursion tree is shown below:

![https://s3-lc-upload.s3.amazonaws.com/users/r0cky2h/image_1536728871.png](https://s3-lc-upload.s3.amazonaws.com/users/r0cky2h/image_1536728871.png)

From the code `if (set.contains(s.substring(0, i)) && wb(s.substring(i), set)) { }`, we can see that only if the wordDict contains the prefix, the recursion function can go down to the next level. So on the figure above, string on the edge means the wordDict contains that string. All the gray node with empty string cannot be reached because if the program reaches one such node, the program will return, which lead to some nodes right to it will not be reached. So the conclusion is for a string with length 4, the recursion tree has 8 nodes (all black nodes), and 8 is 2^(4-1). So to generalize this, for a string with length n, the recursion tree wil have 2^(n-1) nodes, i.e., the time complexity is O(2^n). I will prove this generalization below using mathmatical induction:

![https://s3-lc-upload.s3.amazonaws.com/users/r0cky2h/image_1536729678.png](https://s3-lc-upload.s3.amazonaws.com/users/r0cky2h/image_1536729678.png)

Explanation: the value of a node is the string length. We calculate the number of nodes in the recursion tree for string length=1, 2, ...., n respectively.

For example, when string length=4, the second layer of the recursion tree has three nodes where the string length is 3, 2 and 1 respectively. And the number of subtree rooted at these three nodes have been calculated when we do the mathmatical induction.

So time complexity is O(2^n).

### [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

`tails` is an array storing the smallest tail of all increasing subsequences with length `i+1` in `tails[i]`.

For example, say we have `nums = [4,5,6,3]`, then all the available increasing subsequences are:

`len = 1   :      [4], [5], [6], [3]   => tails[0] = 3
len = 2   :      [4, 5], [5, 6]       => tails[1] = 5
len = 3   :      [4, 5, 6]            => tails[2] = 6`

We can easily prove that tails is a increasing array. Therefore it is possible to do a binary search in tails array to find the one needs update.

Each time we only do one of the two:

`(1) if x is larger than all tails, append it, increase the size by 1
(2) if tails[i-1] < x <= tails[i], update tails[i]`

Doing so will maintain the tails invariant. The the final answer is just the size.

```java
public int lengthOfLIS(int[] nums) {
    int[] tails = new int[nums.length];
    int size = 0;
    for (int x : nums) {
        int i = 0, j = size;
        while (i != j) {
            int m = (i + j) / 2;
            if (tails[m] < x)
                i = m + 1;
            else
                j = m;
        }
        tails[i] = x;
        if (i == size) ++size;
    }
    return size;
}
// Runtime: 2 ms
```

### [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

**Intution :** So Lets start step by step and concentrate on the process:

1. Since we have to make two subset both having equal sum then our first condition is to check whether the sum of given array can be divided in two equal part which is if total sum is odd then partition is not possible at all and if sum is even then there is chance.For example:

	`1.) arr1-> [1,5,11,5]   and     2.) arr2 -> [1,5,3,11] 
	Both arr1 and arr2 has even sum but 1st can be partitioned into ([1,5,5] & [11]) and 2nd can not.`

2.) **Now lets try to visualize it as 0/1 Knapsack Problem:**

- Since in 0/1 knapsack we have 2 choices for each object having value v whether to keep it or not in your kanpsack having certain weight W.
- Same as in this case we have n elements in array and we have two choices to make whether to keep it in subset1 or subset2 (inclusion in one is direct exclusion in other) and weight of knapsack/subset will be sum/2.

3.) So now what our target remain is we have to take care about only one subset because if one subset with weight sum/2 is possible then other subset will surely have the weight sum/2.

4.) So now using subset sum problem code we have to just check if its possible to have a subset having sum = totalSum/2;

**Approach1: Memoization (TLE)**

```java
class Solution {
    boolean mem[][];
    public boolean canPartition(int[] nums) {
        int sum = 0;
        int n = nums.length;
        
        for(int i : nums) sum+=i;
        
        if(sum%2!=0) return false;
        
        sum /= 2;
        
        mem = new boolean[n+1][sum+1];
        
        return subsetSum(nums,0,sum);
    }
    
    boolean subsetSum(int[] nums, int pos, int sum){
        if(sum==0) return true;
        
        else if(pos>=nums.length || sum<0) return false;
        
        if(mem[pos][sum]) return true;
        
        return mem[pos][sum] = subsetSum(nums,pos+1,sum-nums[pos]) ||
                                subsetSum(nums,pos+1,sum);
    }
}
```

- ***A little update:** After reading comments on my post I analyze my memoization code that why its giving TLE so I figured that in subset function if (mem[pos][sum]==true) then I am returning true but if its false then it will keep on computing but the problem was that boolean array automatically initialises array with false..so i cant differentiate... so for that we need to take object boolean array so that it initialises with null or assign null value manually to boolean array.

**Updated Memoization Code: (100% Faster)**

```java
class Solution {
    Boolean mem[][];
    public boolean canPartition(int[] nums) {
        int sum = 0;
        int n = nums.length;
        
        for(int i : nums) sum+=i;
        
        if(sum%2!=0) return false;
        
        sum /= 2;
        
        mem = new Boolean[n+1][sum+1];
        
        return subsetSum(nums,0,sum);
    }
    
    boolean subsetSum(int[] nums, int pos, int sum){
        if(sum==0) return true;
        
        else if(pos>=nums.length || sum<0) return false;
        
        if(mem[pos][sum]!=null) return mem[pos][sum];
        
        return mem[pos][sum] = subsetSum(nums,pos+1,sum-nums[pos]) ||
                                subsetSum(nums,pos+1,sum);
        
        
    }
}
```

**Approach2: Dynamic Programming**

```java
class Solution {
    
    public boolean canPartition(int[] nums) {
        int sum = 0;
        int n = nums.length;
        
        for(int i : nums) sum+=i;
        
        if(sum%2!=0) return false;
        
        sum /= 2;
        
        boolean dp[][] = new boolean[n+1][sum+1];
        
        for(int i=0;i<=n;i++){
            for(int j=0;j<=sum;j++){
                if(i==0 || j==0)
                    dp[i][j] = false;
                else if(nums[i-1] > j)     // if curr sum value is greater than the current element value then just skip(take previous value)
                    dp[i][j] = dp[i-1][j];
                else if(nums[i-1]==j)  // we got required sum
                    dp[i][j] = true;
                else
                    dp[i][j] = dp[i-1][j] || dp[i-1][j-nums[i-1]];
            }
        }
        return dp[n][sum];
        
        
    }
}
```

**Approach3: Space Optimized DP**

**Explanation: Idea behind reverse loop for sum**

- If you observe the 2d DP then dp[i][j] is the value either from dp[i-1][j] or dp[i-1][j-nums[i-1]] and when we converted 2d DP into 1d DP then the thinking was that, dp[i] will have values for one iteration and then again for next iteration we will use that stored values which will act as dp[i-1] for this iteration.
- So now we need value of dp[i-num] that is value from previous index so here is the problem in left to right loop that each time when we enter into new interation we need value from previous iteration but the value will already be updated in this iteartion and we will loss the previous value.
- Thats why using reverse loop.

Example: Lets in first iteration dp array is filled as [2,6,1,8,5]

So now we started from left and upadated 2 as 4 and 6 as 7 and 1 as 5([**4,7,5**,8,5]) and now we reach to 8 and we need dp[1] value but we need the value from previous iteration which we have lost and hence will get the wrong answer.

So move from right to left and use the previous iteration value.

(these are pure random values used in example, so dont think about them just get the example)

```java
class Solution {
    
    public boolean canPartition(int[] nums) {
        int sum = 0;
        int n = nums.length;
        
        for(int i : nums) sum+=i;
        
        if(sum%2!=0) return false;
        
        sum /= 2;
        
        boolean[] dp = new boolean[sum+1];
       
        dp[0] = true;

        for (int j : nums) {
            for (int i = sum; i > 0; i--) {
                if (i >= j) {
                    dp[i] = dp[i] || dp[i-j];
                }
            }
        }

        return dp[sum];
        
        
    }
}
```