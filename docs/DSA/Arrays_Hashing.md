# Arrays and Hashing

## 1. Contains Duplicate

```java
class Solution {

    public boolean containsDuplicate(int[] nums) {
        Set<Integer> uniques = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            if (uniques.contains(nums[i])) {
                return true;
            }
            uniques.add(nums[i]);
        }
        return false;
    }
}
```

## 2. Valid Anagram

```java
class Solution {

    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        int[] store = new int[26];

        for (int i = 0; i < s.length(); i++) {
            store[s.charAt(i) - 'a']++;
            store[t.charAt(i) - 'a']--;
        }

        for (int n : store) if (n != 0) return false;

        return true;
    }
}
```
## 3. Two Sum

```java
class Solution {

    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> prevMap = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            int diff = target - num;

            if (prevMap.containsKey(diff)) {
                return new int[] { prevMap.get(diff), i };
            }

            prevMap.put(num, i);
        }

        return new int[] {};
    }
}
```
## 4. Group Anagrams

```java
class Solution {

    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        int[] store = new int[26];

        for (int i = 0; i < s.length(); i++) {
            store[s.charAt(i) - 'a']++;
            store[t.charAt(i) - 'a']--;
        }

        for (int n : store) if (n != 0) return false;

        return true;
    }
}
```
## 5. Top K Frequent Elements

```java
class Solution1 {

    /**
     * Time Complexity: O(nlog(k))
     * Space Complexity: O(n)
     */
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

class Solution2 {

    /**
     * Time Complexity: O(n)
     * Space Complexity: O(n)
     */
    public int[] topKFrequent(int[] numbers, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int number : numbers) map.put(
            number,
            map.getOrDefault(number, 0) + 1
        );

        int size = map.size();
        int[] keys = new int[size];
        int i = 0;
        for (int key : map.keySet()) keys[i++] = key;

        select(keys, map, 0, size - 1, size - k);
        return Arrays.copyOfRange(keys, size - k, size);
    }

    // Modified implementation of Hoare's selection algorithm:

    private void select(
        int[] keys,
        Map<Integer, Integer> map,
        int left,
        int right,
        int kSmallest
    ) {
        while (left != right) {
            int pivot = partition(keys, map, left, right, (left + right) / 2);

            if (kSmallest == pivot) return;

            if (kSmallest < pivot) right = pivot - 1; else left = pivot + 1;
        }
    }

    private int partition(
        int[] keys,
        Map<Integer, Integer> map,
        int left,
        int right,
        int pivot
    ) {
        int pivotValue = map.get(keys[pivot]);
        swap(keys, pivot, right);
        int index = left;

        for (int i = left; i <= right; i++) if (map.get(keys[i]) < pivotValue) {
            swap(keys, i, index);
            index++;
        }
        swap(keys, right, index);
        return index;
    }

    private void swap(int[] array, int i1, int i2) {
        int temp = array[i1];
        array[i1] = array[i2];
        array[i2] = temp;
    }
}
class Solution3 {
     /**
     * Time Complexity: O(n)
     * Space Complexity: O(n)
     */
     public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> count = new HashMap<>();
        List<Integer> bucket[] = new ArrayList[nums.length + 1];                
        
        for (int num : nums)
            count.merge(num, 1, Integer::sum);
        
        for (int key : count.keySet()){
            int freq = count.get(key);
            if (bucket[freq] == null)
                bucket[freq] = new ArrayList<>();
            bucket[freq].add(key);
        }
        
        int index = 0;
        int[] res = new int[k];
        for (int i = nums.length; i >= 0; i--)
            if (bucket[i] != null)
                for (int val : bucket[i]){
                    res[index++] = val;
                    if(index == k)
                        return res;
                }
        return res;
    }
       

```
## 6. Product of Array Except Self

```java
//Just store the left and right product (Try doing this with extra space first)
//This one is constant space because we are returning the array we created
//In first pass calculate the left product except self and in second calculate the right

class Solution {

    public int[] productExceptSelf(int[] nums) {
        int[] arr = new int[nums.length];
        int right = 1, left = 1;
        for (int i = 0; i < nums.length; i++) {
            arr[i] = left;
            left *= nums[i];
        }
        for (int i = nums.length - 1; i >= 0; i--) {
            arr[i] *= right;
            right *= nums[i];
        }
        return arr;
    }

    public int[] productExceptSelfNumsAsPrefix(int[] nums) {
        int[] output = new int[nums.length];
        output[0] = 1;

        for (int i = 0; i < nums.length - 1; i++) output[i + 1] =
            output[i] * nums[i];

        for (int i = nums.length - 2; i >= 0; i--) {
            output[i] = nums[i + 1] * output[i];
            nums[i] = nums[i] * nums[i + 1];
        }
        return output;
    }
}

```
## 7. Valid Sudoku

```java
class Solution {

    public boolean isValidSudoku(char[][] board) {
        //neetcode solution, slightly modified

        //a set of the characters that we have already come across (excluding '.' which denotes an empty space)
        Set<Character> rowSet = null;
        Set<Character> colSet = null;


        for (int i = 0; i < 9; i++) {
            //reinitialize the sets so we don't carry over found characters from the previous run
            rowSet = new HashSet<>();
            colSet = new HashSet<>();
            for (int j = 0; j < 9; j++) {
                char r = board[i][j];
                char c = board[j][i];
                if (r != '.'){
                    if (rowSet.contains(r)){
                        return false;
                    } else {
                        rowSet.add(r);
                    }
                }
                if (c != '.'){
                    if (colSet.contains(c)){
                        return false;
                    } else {
                        colSet.add(c);
                    }
                }
            }
        }

        //block
        //loop controls advance by 3 each time to jump through the boxes
        for (int i = 0; i < 9; i = i + 3) {
            for (int j = 0; j < 9; j = j + 3) {
                //checkBlock will return true if valid
                if (!checkBlock(i, j, board)) {
                    return false;
                }
            }
        }
        //passed all tests, therefore valid board
        return true;
    }

    public boolean checkBlock(int idxI, int idxJ, char[][] board) {
        Set<Character> blockSet = new HashSet<>();
        //if idxI = 3 and indJ = 0
        //rows = 6 and cols = 3
        int rows = idxI + 3;
        int cols = idxJ + 3;
        //and because i initializes to idxI but only goes to rows, we loop 3 times (once for each row)
        for (int i = idxI; i < rows; i++) {
            //same for columns
            for (int j = idxJ; j < cols; j++) {
                if (board[i][j] == '.') {
                    continue;
                }
                
                if (blockSet.contains(board[i][j])) {
                    return false;
                }

                blockSet.add(board[i][j]);
            }
        }

        return true;
    }
}

```
## 8. Encode and Decode Strings 

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
## 9. Longest Consecutive Sequence

```java
class Solution {

    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        int[] store = new int[26];

        for (int i = 0; i < s.length(); i++) {
            store[s.charAt(i) - 'a']++;
            store[t.charAt(i) - 'a']--;
        }

        for (int n : store) if (n != 0) return false;

        return true;
    }
}
```
