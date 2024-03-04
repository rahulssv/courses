# 15. Greedy

### [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

Analysis of this problem:

Apparently, this is a optimization problem, which can be usually solved by DP. So when it comes to DP, the first thing for us to figure out is the format of the sub problem(or the state of each sub problem). The format of the sub problem can be helpful when we are trying to come up with the recursive relation.

At first, I think the sub problem should look like: `maxSubArray(int A[], int i, int j)`, which means the maxSubArray for A[i: j]. In this way, our goal is to figure out what `maxSubArray(A, 0, A.length - 1)` is. However, if we define the format of the sub problem in this way, it's hard to find the connection from the sub problem to the original problem(at least for me). In other words, I can't find a way to divided the original problem into the sub problems and use the solutions of the sub problems to somehow create the solution of the original one.

So I change the format of the sub problem into something like: `maxSubArray(int A[], int i)`, which means the maxSubArray for A[0:i ] which must has A[i] as the end element. Note that now the sub problem's format is less flexible and less powerful than the previous one because there's a limitation that A[i] should be contained in that sequence and we have to keep track of each solution of the sub problem to update the global optimal value. However, now the connect between the sub problem & the original one becomes clearer:

`maxSubArray(A, i) = maxSubArray(A, i - 1) > 0 ? maxSubArray(A, i - 1) : 0 + A[i];`

And here's the code

```java
public int maxSubArray(int[] A) {
        int n = A.length;
        int[] dp = new int[n];//dp[i] means the maximum subarray ending with A[i];
        dp[0] = A[0];
        int max = dp[0];
        
        for(int i = 1; i < n; i++){
            dp[i] = A[i] + (dp[i - 1] > 0 ? dp[i - 1] : 0);
            max = Math.max(max, dp[i]);
        }
        
        return max;
}
```

### [Jump Game](https://leetcode.com/problems/jump-game/)

The basic idea is this: at each step, we keep track of the furthest reachable index. The nature of the problem (eg. maximal jumps where you can hit a range of targets instead of singular jumps where you can only hit one target) is that for an index to be reachable, each of the previous indices have to be reachable.

Hence, it suffices that we iterate over each index, and If we ever encounter an index that is not reachable, we abort and return false. By the end, we will have iterated to the last index. If the loop finishes, then the last index is reachable.

```java
public boolean canJump(int[] nums) {
    int reachable = 0;
    for (int i=0; i<nums.length; ++i) {
        if (i > reachable) return false;
        reachable = Math.max(reachable, i + nums[i]);
    }
    return true;
}
```

### [Jump Game II](https://leetcode.com/problems/jump-game-ii/)

The main idea is based on greedy. Let's say the range of the current jump is [curBegin, curEnd], curFarthest is the farthest point that all points in [curBegin, curEnd] can reach. Once the current point reaches curEnd, then trigger another jump, and set the new curEnd with curFarthest, then keep the above steps, as the following:

```java
public int jump(int[] A) {
	int jumps = 0, curEnd = 0, curFarthest = 0;
	for (int i = 0; i < A.length - 1; i++) {
		curFarthest = Math.max(curFarthest, i + A[i]);
		if (i == curEnd) {
			jumps++;
			curEnd = curFarthest;
		}
	}
	return jumps;
}
```

### [Gas Station](https://leetcode.com/problems/gas-station/)

The algorithm is pretty easy to understand. Imagine we take a tour around this circle, the only condition that we can complete this trip is to have more fuel provided than costed in total. That's what the first loop does.

If we do have more fuel provided than costed, that means we can always find a start point around this circle that we could complete the journey with an empty tank. Hence, we check from the beginning of the array, if we can gain more fuel at the current station, we will maintain the start point, else, which means we will burn out of oil before reaching to the next station, we will start over at the next station.

```java
public int canCompleteCircuit(int[] gas, int[] cost) {
    int tank = 0;
    for(int i = 0; i < gas.length; i++)
        tank += gas[i] - cost[i];
    if(tank < 0)
        return - 1;
        
    int start = 0;
    int accumulate = 0;
    for(int i = 0; i < gas.length; i++){
        int curGain = gas[i] - cost[i];
        if(accumulate + curGain < 0){
            start = i + 1;
            accumulate = 0;
        }
        else accumulate += curGain;
    }
    
    return start;
}
```

### [Hand of Straights](https://leetcode.com/problems/hand-of-straights/)

**TreeMap:**

```java
class Solution {
    public boolean isNStraightHand(int[] hand, int W) {
        if (hand.length % W != 0) return false;
        
        TreeMap<Integer, Integer> map = new TreeMap<>();    
        for (int h : hand) map.put(h, map.getOrDefault(h, 0) + 1);
    
        
        while (map.size() > 0) {
            int val = map.firstKey();
            for (int i = val; i < val + W; i++) {
                if (!map.containsKey(i)) return false;
                
                map.put(i, map.get(i) - 1);
                if (map.get(i) == 0) map.remove(i);
            }
        }
        
        return true;
    }
}
```

**PriorityQueue (min heap):**

```java
class Solution {
    public boolean isNStraightHand(int[] hand, int W) {
        if (hand.length % W != 0) return false;

        PriorityQueue<Integer> heap = new PriorityQueue<>();
        for (int h : hand) heap.offer(h);

        while (!heap.isEmpty()) {
            int val = heap.peek();
            for (int i = val; i < val + W; i++) {
                if (!heap.remove(i)) return false;
            }  
        }
        return true;
    }
}
```

### [Merge Triplets to Form Target Triplet](https://leetcode.com/problems/merge-triplets-to-form-target-triplet/)

Consider only triplets that do not exceed the target in any dimension.

Greedily apply the operation using all those triplets. That way, `res` will get as close to a target as possible.

```java
public boolean mergeTriplets(int[][] triplets, int[] t) {
    int[] res = new int[3];
    for (var s : triplets)
        if (s[0] <= t[0] && s[1] <= t[1] && s[2] <= t[2])
            res = new int[]{ Math.max(res[0], s[0]), Math.max(res[1], s[1]), Math.max(res[2], s[2]) };
    return Arrays.equals(res, t);
}
```

### [Partition Labels](https://leetcode.com/problems/partition-labels/)

`TIME COMPLEXITY & SPACE COMPLEXITY IS O(N)`

`TIME COMPLEXITY IS O(N) BECAUSE YOU ARE VISITING ANY CHARACTER ONLY ONCE
UPDATION OF OUTER LOOP POINTER CLEARLY SHOWS THE PROOF WHERE YOU ARE VISITING CHARACTERS ONLY ONCE.`

`YOU CAN REDUCE SPACE COMPLEXITY BY USING ARRAY OF SIZE 26.`

- `FIRST STEP IN SOLVING THESE TYPE OF QUESTIONS IS TO NOTE WHERE OUR CHARACTER HAS IT'S LAST APPEARANCE.
* USE HASMAP TO STORE IT.
* WE HAVE TO TRAVERSE THE WHOLE STRING SO WE MAINTAIN A LOOP FOR IT.
* AND WE FIND THE LASTMOST APPEARANCE OF THAT CHARACTER AND RUN OVER THEM.
* IF WE FIND ANY INDEX OF ANY CHARACTER GREATER THAN THE CURRENT ONE, WE UPDATE THE NEW MAXEND.
* ADD THE LENGTH TO LIST (MAXEND - OUTERLOOP + 1);
* UPDATE OUR OUTER LOOP TO FIND OTHER LENGTH.`

```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        int n = s.length();
        List<Integer> l = new ArrayList<>();
        HashMap<Character, Integer> map = new HashMap<>();
        
        //Store the last indexes of the characters.
        for (int i = 0; i < n; i++) map.put(s.charAt(i), i);

        int outerLoop = 0;
        while (outerLoop < n) {
            int maxEnd = map.get(s.charAt(outerLoop)), innerLoop = outerLoop + 1;
            while (innerLoop < maxEnd) {
                int curr = map.get(s.charAt(innerLoop));
                if (curr > maxEnd) {
                    maxEnd = curr;
                }
                innerLoop++;
            }
            l.add(maxEnd - outerLoop + 1);
            outerLoop = maxEnd + 1;
        }

        return l;
    }
}
```

### [Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)

**Problem 1: Check Valid Parenthesis of a string containing only two types of characters: '(', ')'**

```java
class Solution {
    public boolean checkValidString(String s) {
        int openCount = 0;
        for (char c : s.toCharArray()) {
            if (c == '(') {
                openCount++;
            } else if (c == ')') {
                openCount--;
            }
            if (openCount < 0) return false;    // Currently, don't have enough open parentheses to match close parentheses-> Invalid
                                                // For example: ())(
        }
        return openCount == 0; // Fully match open parentheses with close parentheses
    }
}
```

**Problem 2: Check Valid Parenthesis of a string containing only three types of characters: '(', ')', '*'**

Example:

![https://assets.leetcode.com/users/hiepit/image_1587291349.png](https://assets.leetcode.com/users/hiepit/image_1587291349.png)

```java
class Solution {
    public boolean checkValidString(String s) {
        int cmin = 0, cmax = 0; // open parentheses count in range [cmin, cmax]
        for (char c : s.toCharArray()) {
            if (c == '(') {
                cmax++;
                cmin++;
            } else if (c == ')') {
                cmax--;
                cmin--;
            } else if (c == '*') {
                cmax++; // if `*` become `(` then openCount++
                cmin--; // if `*` become `)` then openCount--
                // if `*` become `` then nothing happens
                // So openCount will be in new range [cmin-1, cmax+1]
            }
            if (cmax < 0) return false; // Currently, don't have enough open parentheses to match close parentheses-> Invalid
                                        // For example: ())(
            cmin = Math.max(cmin, 0);   // It's invalid if open parentheses count < 0 that's why cmin can't be negative
        }
        return cmin == 0; // Return true if can found `openCount == 0` in range [cmin, cmax]
    }
}
```

Complexity

- Time: `O(n)`
- Space: `O(1)`