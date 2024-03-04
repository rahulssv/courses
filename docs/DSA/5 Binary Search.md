# 5. Binary Search

### [Binary Search](https://leetcode.com/problems/binary-search/)

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return -1;
    }
}
```

### [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

```java
class Solution {
    public boolean searchMatrix(int[][] m, int target) {
        if (m == null || m.length == 0) {
            return false;
        }
        int start = 0, rows = m.length, cols = m[0].length;
        int end = rows * cols - 1;
        while (start <= end) {
            int mid = (start + end) / 2;
            if (m[mid / cols][mid % cols] == target) {
                return true;
            } else if (m[mid / cols][mid % cols] < target) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return false;
    }
}
```

### [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int left = 1;
        int right = 1000000000;
        int mid = 0;
        while (left < right) {
            mid = (right + left) / 2;
            if (canEatAtTime(piles, mid, h)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }

    public boolean canEatAtTime(int[] piles, int k, int h) {
        int hours = 0;
        for (int pile : piles) {
            int div = (pile + k - 1) / k;
            hours += div;

        }
        return hours <= h;

    }

}
```

### [Find Minimum In Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        while (l < r) {
            int mid = (l + r) / 2;
            if (nums[mid] < nums[r]) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return nums[l];
    }
}
```

### [Search In Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

```java
class Solution {
    public int search(int[] nums, int target) {
        int l = 0;
        int h = nums.length - 1;
        while (l < h) {
            int mid = (l + h) / 2;
            if ((nums[0] > target) ^ (nums[0] > nums[mid]) ^ (target > nums[mid])) {
                l = mid + 1;
            } else {
                h = mid;
            }

        }
        return l == h && nums[l] == target ? l : -1;
    }
}
```

### [Time Based Key Value Store](https://leetcode.com/problems/time-based-key-value-store/)

```java
class Pair {
    String value;
    int timestamp;

    Pair(String value, int timestamp) {
        this.value = value;
        this.timestamp = timestamp;
    }
}

class TimeMap {

    private HashMap<String, ArrayList<Pair>> hm;

    public TimeMap() {
        hm = new HashMap<String, ArrayList<Pair>>();
    }

    public void set(String key, String value, int timestamp) {
        if (hm.containsKey(key)) {
            hm.get(key).add(new Pair(value, timestamp));
        } else {
            ArrayList<Pair> arr = new ArrayList<Pair>();
            arr.add(new Pair(value, timestamp));
            hm.put(key, arr);
        }
    }

    public String get(String key, int timestamp) {
        String crr = "";
        if (hm.containsKey(key)) {
            ArrayList<Pair> arr2 = hm.get(key);
            int l = 0;
            int h = arr2.size() - 1;
            while (l <= h) {
                int mid = (l + h) / 2;
                int ts = arr2.get(mid).timestamp;
                if (ts == timestamp) {
                    return arr2.get(mid).value;
                } else if (ts < timestamp) {
                    crr = arr2.get(l).value;
                    l = mid + 1;

                } else {
                    h = mid - 1;
                }
            }
        }
        return crr;

    }
}

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap obj = new TimeMap();
 * obj.set(key,value,timestamp);
 * String param_2 = obj.get(key,timestamp);
 */
```

### [Median
of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

```java
/*Brute-force solution (Linear)*/
/*
// Runtime: O(m+n)
// Extra Space: O(m+n)
// 
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        int[] nums = new int[m+n];
        int i = 0, j = 0;
        int k = 0;
        while (i<m && j<n) {
            if (nums1[i]<nums2[j]) nums[k++] = nums1[i++];
            else nums[k++] = nums2[j++];
        }
        for (; i<m; i++) nums[k++] = nums1[i];
        for (; j<n; j++) nums[k++] = nums2[j];
        if ((m+n)%2 == 0) {
            return ((float)nums[(m+n-1)/2]+(float)nums[(m+n)/2])/(float)2;
        } else return (float)nums[(m+n-1)/2];
    }
}
*/
/* Optimized solution (Logarithmic) */

// Runtime: O(log(min(m,n)))
// Extra Space: O(1)

class Solution {

    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;

        if (m > n) {
            return findMedianSortedArrays(nums2, nums1);
        }

        int total = m + n;
        int half = (total + 1) / 2;

        int left = 0;
        int right = m;

        var result = 0.0;

        while (left <= right) {
            int i = left + (right - left) / 2;
            int j = half - i;

            // get the four points around possible median
            int left1 = (i > 0) ? nums1[i - 1] : Integer.MIN_VALUE;
            int right1 = (i < m) ? nums1[i] : Integer.MAX_VALUE;
            int left2 = (j > 0) ? nums2[j - 1] : Integer.MIN_VALUE;
            int right2 = (j < n) ? nums2[j] : Integer.MAX_VALUE;

            // partition is correct
            if (left1 <= right2 && left2 <= right1) {
                // even
                if (total % 2 == 0) {
                    result =
                        (Math.max(left1, left2) + Math.min(right1, right2)) /
                        2.0;
                    // odd
                } else {
                    result = Math.max(left1, left2);
                }
                break;
            }
            // partition is wrong (update left/right pointers)
            else if (left1 > right2) {
                right = i - 1;
            } else {
                left = i + 1;
            }
        }

        return result;
    }
}

```