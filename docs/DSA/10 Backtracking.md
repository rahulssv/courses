# 10. Backtracking

### [Subsets](https://leetcode.com/problems/subsets/)

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        backtrack(list, new ArrayList<Integer>(), nums, 0);
        return list;
    }

    public void backtrack(List<List<Integer>> list, ArrayList<Integer> tempList, int[] nums, int start) {
        list.add(new ArrayList<>(tempList));
        for (int i = start; i < nums.length; i++) {
            tempList.add(nums[i]);
            backtrack(list, tempList, nums, i + 1);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

### [Combination Sum](https://leetcode.com/problems/combination-sum/)

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> list = new ArrayList<>();
        // Arrays.sort(candidates);
        backtrack(candidates, target, list, new ArrayList<Integer>(), 0);
        return list;
    }

    public void backtrack(int[] candidates, int target, List<List<Integer>> list, ArrayList<Integer> tempList,
            int start) {
        if (target < 0)
            return;
        else if (target == 0) {
            list.add(new ArrayList<>(tempList));

        } else {
            for (int i = start; i < candidates.length; i++) {

                tempList.add(candidates[i]);
                backtrack(candidates, target - candidates[i], list, tempList, i);
                tempList.remove(tempList.size() - 1);
            }
        }

    }
}
```

### [Permutations](https://leetcode.com/problems/permutations/)

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        backTrack(list, new ArrayList<Integer>(), nums);
        return list;
    }

    public void backTrack(List<List<Integer>> list, ArrayList<Integer> tempList, int[] nums) {
        if (tempList.size() == nums.length) {
            list.add(new ArrayList<>(tempList));
        }

        for (int i = 0; i < nums.length; i++) {
            if (tempList.contains(nums[i])) {
                continue;
            }
            tempList.add(nums[i]);
            backTrack(list, tempList, nums);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

### [Subsets II](https://leetcode.com/problems/subsets-ii/)

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        backTrack(list, new ArrayList<Integer>(), nums, 0);
        return list;

    }

    public void backTrack(List<List<Integer>> list, ArrayList<Integer> tempList, int[] nums, int start) {
        if (!list.contains(tempList)) {
            list.add(new ArrayList<>(tempList));
        }

        for (int i = start; i < nums.length; i++) {
            // if(tempList.contains(nums[i])){
            // continue;
            // }
            tempList.add(nums[i]);
            backTrack(list, tempList, nums, i + 1);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

### [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(list, new ArrayList<>(), candidates, target, 0);
        return list;
    }

    public void backtrack(List<List<Integer>> list, ArrayList<Integer> tempList, int[] candidates, int remaining,
            int start) {
        if (remaining < 0)
            return;
        else if (remaining == 0) {
            list.add(new ArrayList<>(tempList));
        } else {
            for (int i = start; i < candidates.length; i++) {
                if (i > start && candidates[i] == candidates[i - 1])
                    continue;
                tempList.add(candidates[i]);
                backtrack(list, tempList, candidates, remaining - candidates[i], i + 1);
                tempList.remove(tempList.size() - 1);
            }
        }

    }
}
```

### [Word Search](https://leetcode.com/problems/word-search/)

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == word.charAt(0) && backtrack(board, word, 0, i, j))
                    return true;
            }
        }
        return false;

    }

    public boolean backtrack(char[][] board, String word, int index, int i, int j) {
        if (index >= word.length()) {
            return true;

        }
        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length || board[i][j] == '0'
                || board[i][j] != word.charAt(index))
            return false;
        char temp = board[i][j];
        board[i][j] = '0';
        if (backtrack(board, word, index + 1, i + 1, j) ||
                backtrack(board, word, index + 1, i - 1, j) ||
                backtrack(board, word, index + 1, i, j + 1) ||
                backtrack(board, word, index + 1, i, j - 1)) {
            return true;
        }
        board[i][j] = temp;

        return false;

    }

}
```

### [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> list = new ArrayList<>();
        backtrack(list, new ArrayList<String>(), s, 0);
        return list;
    }

    public void backtrack(List<List<String>> list, ArrayList<String> tempList, String s, int start) {
        if (start == s.length()) {
            list.add(new ArrayList<>(tempList));
            return;
        }

        for (int i = start; i < s.length(); i++) {
            if (isPalidrome(s, start, i)) {
                tempList.add(s.substring(start, i + 1));
                backtrack(list, tempList, s, i + 1);
                tempList.remove(tempList.size() - 1);
            }
        }
    }

    public boolean isPalidrome(String s, int low, int high) {
        while (low < high) {
            if (s.charAt(low) != s.charAt(high))
                return false;
            low++;
            high--;
        }
        return true;
    }
}
```

### [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

```java
class Solution {
    public List<String> letterCombinations(String digits) {
        List<String> list = new ArrayList<>();
        if (digits.equals("")) {
            return list;
        }
        String[] letters = new String[] { "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz" };
        backtrack(list, new StringBuilder(), letters, digits, 0);
        return list;
    }

    public void backtrack(List<String> list, StringBuilder str, String[] letters, String digits, int index) {
        if (index == digits.length()) {
            list.add(str.toString());
            return;
        }
        int digit = digits.charAt(index) - '0';
        String letter = letters[digit - 2];
        for (int i = 0; i < letter.length(); i++) {
            str.append(letter.charAt(i));
            backtrack(list, str, letters, digits, index + 1);
            str.deleteCharAt(str.length() - 1);
        }
    }
}
```

### [N Queens](https://leetcode.com/problems/n-queens/)

```java
class Solution {
    HashSet<Integer> cols = new HashSet<Integer>();
    HashSet<Integer> diag1 = new HashSet<Integer>();
    HashSet<Integer> diag2 = new HashSet<Integer>();

    public List<List<String>> solveNQueens(int n) {
        List<List<String>> lists = new ArrayList<>();
        backtrack(lists, new ArrayList<String>(), n, 0);
        return lists;
    }

    public void backtrack(List<List<String>> lists, List<String> list, int n, int row) {
        if (row == n) {
            lists.add(new ArrayList<>(list));
            return;
        }
        for (int i = 0; i < n; i++) {
            if (cols.contains(i) || diag1.contains(row + i) || diag2.contains(row - i))
                continue;
            char[] charArr = new char[n];
            Arrays.fill(charArr, '.');
            charArr[i] = 'Q';
            list.add(new String(charArr));
            cols.add(i);
            diag1.add(row + i);
            diag2.add(row - i);
            backtrack(lists, list, n, row + 1);
            list.remove(list.size() - 1);
            cols.remove(i);
            diag1.remove(row + i);
            diag2.remove(row - i);
        }
    }
}
```