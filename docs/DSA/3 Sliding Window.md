# 3. Sliding Window

### [Best Time to Buy And Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```java
class Solution {
    public int maxProfit(int[] prices) {

        int min = Integer.MAX_VALUE;
        int profit = 0;
        int maxProfit = 0;
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < min) {
                min = prices[i];
            }
            profit = prices[i] - min;
            if (profit > maxProfit) {
                maxProfit = profit;
            }
        }
        return maxProfit;
    }
}
```

### [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> cs = new HashSet<Character>();
        int maxLength = 0;
        int left = 0;
        for (int i = 0; i < s.length(); i++) {
            if (cs.add(s.charAt(i))) {
                maxLength = Math.max(maxLength, i - left + 1);
            } else {
                while (!cs.add(s.charAt(i))) {
                    cs.remove(s.charAt(left));
                    left++;
                }
            }
        }
        return maxLength;
    }
}
```

### [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

```java
class Solution {
    public int characterReplacement(String s, int k) {
        int[] arr = new int[26];
        int l = 0;
        int max = 0;
        int res = 0;
        for (int r = 0; r < s.length(); r++) {

            max = Math.max(max, ++arr[s.charAt(r) - 'A']);
            if (r - l + 1 - max > k) {
                arr[s.charAt(l) - 'A']--;
                l++;
            }
            res = Math.max(res, r - l + 1);
        }
        return res;
    }
}
```

### [Permutation In String](https://leetcode.com/problems/permutation-in-string/)

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length())
            return false;
        int[] arr1 = new int[26];
        int[] arr2 = new int[26];
        for (int i = 0; i < s1.length(); i++) {
            arr1[s1.charAt(i) - 'a']++;
            arr2[s2.charAt(i) - 'a']++;
        }
        if (Arrays.equals(arr1, arr2))
            return true;
        int end = s1.length();
        int begin = 0;
        while (end < s2.length()) {
            arr2[s2.charAt(begin) - 'a']--;
            arr2[s2.charAt(end) - 'a']++;

            if (Arrays.equals(arr1, arr2))
                return true;
            end++;
            begin++;
        }
        return false;
    }
}
```

### [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

```java
class Solution {
    public String minWindow(String s, String t) {
        int[] count = new int[128];
        for (char i : t.toCharArray()) {
            count[i]++;
        }
        String ws = "";
        int wl = 0, wr = 0, cfw = 0, tc = t.length(), minw = Integer.MAX_VALUE;
        char[] src = s.toCharArray();
        while (wr < s.length()) {
            int cc = src[wr];
            count[cc]--;
            if (count[cc] >= 0) {
                cfw++;
            }
            while (cfw == tc) {
                int cwl = wr - wl + 1;
                if (minw > cwl) {
                    minw = cwl;
                    ws = s.substring(wl, wr + 1);
                }
                count[src[wl]]++;
                if (count[src[wl]] > 0) {
                    cfw--;
                }
                wl++;
            }
            wr++;
        }
        return ws;
    }
}
```

```java
class Solution {
    public String minWindow(String s, String t) {
        int[] count = new int[128];

        // Count the characters in t
        for (char ch : t.toCharArray()) count[ch]++;

        char[] sourceStr = s.toCharArray();
        String windowString = "";
        int windowLeft = 0, windowRight = 0, charsFoundInWindow = 0,
                totalCharsToFind = t.length(), minWindowLen = Integer.MAX_VALUE;
        while (windowRight < sourceStr.length) {
            int currentChar = sourceStr[windowRight];
            // Reduce the count of current character
            count[currentChar]--;
            // If current character's count is greater than or equal to 0 if it was also present in target string t
            // and we can say that we have found that character in current window so we increment charsFoundInWindow
            if (count[currentChar] >= 0) {
                charsFoundInWindow++;
            }

            // If we found a window containing all characters of t, find if it's smaller than the smallest window
            // If yes, store the window in windowString to return finally.
            while (charsFoundInWindow == totalCharsToFind) {
                int currentWindowLen = windowRight - windowLeft + 1;
                if(minWindowLen > currentWindowLen) {
                    minWindowLen = currentWindowLen;
                    windowString = s.substring(windowLeft, windowRight + 1);
                }
                // Now we need to reduce the window size from left to further look for smaller windows.
                // The current leftmost character was already visited by right pointer windowRight earlier
                // and we had reduced its count in count[]. So now we increment it because
                // we need the count of that character in the remaining window.
                count[sourceStr[windowLeft]]++;
                // Now if the last character is greater than 0, it means that character was present in t but
                // is not present in current window so we have to decrement charsFoundInWindow
                if (count[sourceStr[windowLeft]] > 0) {
                    charsFoundInWindow--;
                }
                windowLeft++;
            }
            windowRight++;
        }
        return windowString;
    }
}
```

### [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

```java
class Solution {

    public int[] maxSlidingWindow(int[] nums, int k) {
        int[] ans = new int[nums.length - k + 1];
        int j = 0;
        Deque<Integer> q = new LinkedList<>();
        for (int i = 0; i < nums.length; i++) {
            if (!q.isEmpty() && q.peekFirst() < i - k + 1) q.pollFirst();
            while (!q.isEmpty() && nums[i] > nums[q.peekLast()]) q.pollLast();
            q.offer(i);
            if (i >= k - 1) ans[j++] = nums[q.peekFirst()];
        }
        return ans;
    }
}
```