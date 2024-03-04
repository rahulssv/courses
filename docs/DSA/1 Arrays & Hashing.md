# 1. Arrays & Hashing

### [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> s = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            if (!s.add(nums[i])) {
                return true;
            }
        }
        return false;
    }
}
```

### [Valid Anagram](https://leetcode.com/problems/valid-anagram/)

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length()!=t.length()){
            return false;
        }
        int[] store = new int[26];
        for(int i=0;i<s.length();i++){
            store[s.charAt(i)-'a']++;
            store[t.charAt(i)-'a']--;
        }
        for(int i:store){
            if(i!=0){
                return false;
            }
        }
        return true;
    }
}
```

### [Two Sum](https://leetcode.com/problems/two-sum/)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] arr = new int[2];
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    arr[0] = i;
                    arr[1] = j;
                }
            }
        }
        return arr;
    }
}
```

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> hm=new HashMap<>();
        for(int i=0;i<nums.length;i++){
            if(hm.containsKey(target-nums[i])){
                
                return new int[]{hm.get(target-nums[i]),i};
            }
            hm.put(nums[i],i);
        }
        return new int[1];
    }
}
```

### [Group Anagrams](https://leetcode.com/problems/group-anagrams/)

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String,List<String>> anagrams= new HashMap<>();
        for(String word : strs){
            char[] charWord=word.toCharArray();
            Arrays.sort(charWord);
            String str=new String(charWord);
            if(!anagrams.containsKey(str)){
                anagrams.put(str, new ArrayList<>());
            }
            anagrams.get(str).add(word);
        }
        return new ArrayList<>(anagrams.values());
    }
}
```

### [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

```java
public class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        int[] arr = new int[k];
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int num : nums) map.put(num, map.getOrDefault(num, 0) + 1);
        PriorityQueue<Map.Entry<Integer, Integer>> pq = new PriorityQueue<>(
                (a, b) ->
            a.getValue() - b.getValue()
        );
        for (Map.Entry<Integer, Integer> it : map.entrySet()) {
            pq.add(it);
            if (pq.size() > k) pq.poll();
        }
        int i = k;
        while (!pq.isEmpty()) {
            arr[--i] = pq.poll().getKey();
        }
        return arr;
    }
}
```

### [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n=nums.length;
        int left=1;
        int right=1;
        int[] arr= new int[n];
        for(int i=0;i<n;i++){
            arr[i]=left;
            left*=nums[i];
        }
        for(int j=n-1;j>=0;j--){
            arr[j]*=right;
            right*=nums[j];
        }
        return arr;
    }
}
```

### [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        
        for(int i=0;i<9;i++){
            Set<Character> row=new HashSet<Character>();
            Set<Character> col=new HashSet<Character>();
            for(int j=0;j<9;j++){
                if(board[i][j]!='.'){
                    if(!row.add(board[i][j])){
                        return false;
                    }
                    
                }
                if(board[j][i]!='.'){
                    if(!col.add(board[j][i])){
                        return false;
                    }
                }
                
            }
        }

        for (int k=0;k<9;k=k+3){
            for(int l=0;l<9;l=l+3){
                if(!sudokuBox(k,l,board)){
                    return false;
                }
            }
        }
        return true;
    }
    public static boolean sudokuBox(int x, int y, char[][] box){
        Set<Character> cube =new HashSet<Character>();
        for(int i=x;i<x+3;i++){
            
            for(int j=y;j<y+3;j++){
                if(box[i][j]!='.'){
                    if(!cube.add(box[i][j])){
                    return false;
                }
                }
                
            }
        }
        return true;
    }
}
```

### [Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/)

```java
public class Solution {

    public String encode(List<String> strs) {
        StringBuilder encodedString = new StringBuilder();
        for (String str : strs) {
            encodedString.append(str.length()).append("#").append(str);
        }
        return encodedString.toString();
    }

    public List<String> decode(String str) {
        List<String> list = new ArrayList<>();
        int i = 0;
        while (i < str.length()) {
            int j = i;
            while (str.charAt(j) != '#') j++;

            int length = Integer.valueOf(str.substring(i, j));
            i = j + 1 + length;
            list.add(str.substring(j + 1, i));
        }
        return list;
    }
}

```

### [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

```java
class Solution {
    public int longestConsecutive(int[] nums) {
       if (nums.length == 0) return 0;
       HashSet<Integer> hs = new HashSet<>();
       for(int num:nums) hs.add(num);
       int longest =1;
       for(int num: nums ){
           //check if the num is the start of a sequence by checking if left exists
           if(!hs.contains(num-1)){ // start of a sequence
                int count =1;
                while(hs.contains(num + 1)){ // check if hs contains next no.
                    num++;
                    count++;
                }
                longest = Math.max(longest, count);
                
           }
           if(longest > nums.length/2) break;

       }
       return longest;
    }
}
```