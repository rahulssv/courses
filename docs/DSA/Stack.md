# Stack

### [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack<Character>();
        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                st.push(c);

            } else {
                if (st.isEmpty()) {
                    return false;
                }
                char t = st.peek();
                if (t == '(' && c == ')' || t == '{' && c == '}' || t == '[' && c == ']') {
                    st.pop();
                } else {
                    return false;
                }
            }
        }
        return st.isEmpty();
    }
}
```

### [Min Stack](https://leetcode.com/problems/min-stack/)

```java
class MinStack {
    Stack<Node> s;
    int min;
    public MinStack() {
        s=new Stack();
        min=Integer.MAX_VALUE;
    }
    
    public void push(int val) {
        if(s.isEmpty()){
            min=val;
        }
        else{
            min=Math.min(val,s.peek().min);
        }
        s.push(new Node(val,min));
    }
    
    public void pop() {
        s.pop();
    }
    
    public int top() {
        return s.peek().val;
    }
    
    public int getMin() {
        return s.peek().min;
    }
}
class Node{
    int min;
    int val;
    Node(int val,int min){
        this.val=val;
        this.min=min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

### [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

```java
class Solution {
    public int evalRPN(String[] tokens) {
        int[] stack = new int[tokens.length];
        int top = 0;
        for (String s : tokens) {
            char c = s.charAt(0);
            if (c == '+') {
                int b = stack[--top];
                int a = stack[--top];
                stack[top++] = a + b;
            } else if (c == '-' && s.length() == 1) {
                int b = stack[--top];
                int a = stack[--top];
                stack[top++] = a - b;
            } else if (c == '/') {
                int b = stack[--top];
                int a = stack[--top];
                stack[top++] = a / b;
            } else if (c == '*') {
                int b = stack[--top];
                int a = stack[--top];
                stack[top++] = a * b;
            } else {
                stack[top++] = Integer.parseInt(s);
            }
        }
        return stack[0];
    }
}
```

### [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> lts = new ArrayList<String>();
        String c = "";
        int coo = 0;
        int coc = 0;
        backtrack(lts, c, coo, coc, n);
        return lts;
    }

    public void backtrack(List<String> lts, String c, int coo, int coc, int n) {
        if (coo == n && coc == n) {
            lts.add(c);
            return;
        }
        if (coo < n) {
            backtrack(lts, c + "(", coo + 1, coc, n);
        }
        if (coc < coo) {
            backtrack(lts, c + ")", coo, coc + 1, n);
        }
    }
}
```

### [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int[] ans = new int[temperatures.length];
        Stack<Integer> stack = new Stack<Integer>();
        for (int i = temperatures.length - 1; i >= 0; i--) {
            if (stack.isEmpty()) {
                stack.push(i);
                ans[i] = 0;
            } else {
                while (!stack.isEmpty() && temperatures[i] >= temperatures[stack.peek()]) {
                    stack.pop();
                }
                if (stack.isEmpty()) {
                    ans[i] = 0;
                } else {
                    ans[i] = stack.peek() - i;
                }
                stack.push(i);
            }
        }
        return ans;
    }
}
```

### [Car Fleet](https://leetcode.com/problems/car-fleet/)

```java
class Solution {
    public int carFleet(int target, int[] position, int[] speed) {
        Map<Integer, Double> map = new TreeMap<>(Collections.reverseOrder());
        for (int i = 0; i < position.length; i++) {
            map.put(position[i], (double) (target - position[i]) / speed[i]);
        }
        int fleet = 0;
        double cur = 0;
        for (double time : map.values()) {
            if (time > cur) {
                cur = time;
                fleet++;
            }
        }
        return fleet;
    }
}
```

### [Largest Rectangle In Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int len = heights.length;
        Stack<Integer> s = new Stack<>();
        int maxArea = 0;
        for (int i = 0; i <= len; i++) {
            int h = (i == len ? 0 : heights[i]);
            if (s.isEmpty() || h >= heights[s.peek()]) {
                s.push(i);
            } else {
                int top = s.pop();
                maxArea = Math.max(maxArea, heights[top] * (s.isEmpty() ? i : i - 1 - s.peek()));
                i--;
            }
        }
        return maxArea;
    }
}
```