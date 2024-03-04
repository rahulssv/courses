# 2. Two Pointers

### [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

```java
class Solution {
    public boolean isPalindrome(String s) {
        s=s.replaceAll("[^a-zA-Z0-9]+", "");
        s=s.toLowerCase();
        StringBuilder s1=new StringBuilder(s);
        if(s.equals(s1.reverse().toString())){
            return true;
        }
        else{
            return false;
        }
    }
}
```

### [Two Sum II Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int low=0,high=nums.length-1;
        while(low<high){
            if(nums[low]+nums[high]==target){
                return new int[]{low+1,high+1};
            }else if(nums[low]+nums[high]<target){
                low++;
            }else{
                high--;
            }
        }
        return new int[0];
    }
}
```

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        HashMap<Integer,Integer> h=new HashMap<>();
        for(int i=0;i<numbers.length;i++){
            if(h.containsKey(target-numbers[i])){
                return new int[]{h.get(target-numbers[i]),i+1};
            }
            else{
                h.put(numbers[i],i+1);
            }
        }
        return numbers;
    }
}
```

### [3Sum](https://leetcode.com/problems/3sum/)

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {

        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int j = i + 1;
            int k = nums.length - 1;
            while (j < k) {
                int sum = nums[i] + nums[j] + nums[k];
                if (sum == 0) {

                    ans.add(Arrays.asList(nums[i], nums[j], nums[k]));

                    while (j < k && nums[j] == nums[j + 1]) {
                        j++;
                    }
                    while (j < k && nums[k] == nums[k - 1]) {
                        k--;
                    }
                    j++;
                    k--;
                } else if (sum < 0) {
                    j++;
                } else {
                    k--;
                }
            }

        }
        return ans;
    }

}
```

### [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int max = 0;
        while (left < right) {
            int length = Math.min(height[left], height[right]);
            int width = right - left;
            int area = length * width;
            max = Math.max(max, area);
            if (height[left] < height[right]) {
                left++;
            } else if (height[left] > height[right]) {
                right--;
            } else {
                left++;
                right--;
            }
        }
        return max;
    }
}
```

### [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

```java
class Solution {
    public int trap(int[] h) {
        if (h == null || h.length < 2)
            return 0;
        Stack<Integer> s = new Stack<Integer>();
        int i = 0;
        int water = 0;
        int mh = 0;
        while (i < h.length) {
            if (s.isEmpty() || h[i] < h[s.peek()]) {
                s.push(i++);
            } else {
                int pre = s.pop();
                if (!s.empty()) {
                    mh = Math.min(h[s.peek()], h[i]);
                    water += (mh - h[pre]) * (i - s.peek() - 1);
                }

            }
        }
        return water;
    }
}
```