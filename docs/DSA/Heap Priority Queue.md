# Heap / Priority Queue

### [Kth Largest Element In a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

```java
class KthLargest {
    PriorityQueue<Integer> q;
    int k;

    public KthLargest(int k, int[] nums) {
        this.q = new PriorityQueue<>(k);
        this.k = k;
        for (int val : nums) {
            add(val);
        }
    }

    public int add(int val) {
        if (q.size() < k) {
            q.offer(val);
        } else if (q.peek() < val) {
            q.poll();
            q.offer(val);
        }
        return q.peek();
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```

### [Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)

```java
class Solution {
    PriorityQueue<Integer> q;

    public int lastStoneWeight(int[] stones) {
        q = new PriorityQueue<Integer>(Collections.reverseOrder());
        for (int stone : stones) {
            q.offer(stone);
        }

        while (q.size() > 1) {
            q.offer(q.poll() - q.poll());

        }
        return q.peek();
    }
}
```

### [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        Arrays.sort(points, Comparator.comparing(point -> point[0] * point[0] + point[1] * point[1]));

        return Arrays.copyOfRange(points, 0, k);
    }
}
```

### [Kth Largest Element In An Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> q = new PriorityQueue<Integer>(k);
        for (int num : nums) {
            if (q.size() < k) {
                q.offer(num);
            } else {
                if (num > q.peek()) {
                    q.poll();
                    q.offer(num);
                }
            }
        }
        return q.peek();

    }
}
```

### [Task Scheduler](https://leetcode.com/problems/task-scheduler/)

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int[] count = new int[26];
        int max = 0;
        int maxcount = 0;
        for (char c : tasks) {
            count[c - 'A']++;
            max = Math.max(max, count[c - 'A']);
        }
        for (int i : count) {
            if (i == max) {
                maxcount++;
            }
        }
        return Math.max(tasks.length, (max - 1) * (n + 1) + maxcount);
    }
}
```

### [Design Twitter](https://leetcode.com/problems/design-twitter/)

```java
class Tweet {
    int tweetId;
    int userId;

    public Tweet(int t, int u) {
        tweetId = t;
        userId = u;
    }
}

class User {
    int userId;
    HashSet<Integer> follows;

    public User(int u) {
        userId = u;
        follows = new HashSet<>();
    }
}

class Twitter {
    ArrayList<Tweet> tweets;
    HashMap<Integer, User> users;

    public Twitter() {
        tweets = new ArrayList<Tweet>();
        users = new HashMap<Integer, User>();
    }

    public void postTweet(int userId, int tweetId) {
        if (!users.containsKey(userId)) {
            users.put(userId, new User(userId));
        }
        tweets.add(new Tweet(tweetId, userId));
    }

    public List<Integer> getNewsFeed(int userId) {
        if (!users.containsKey(userId)) {
            users.put(userId, new User(userId));
        }
        int i = tweets.size() - 1;
        List<Integer> ans = new ArrayList<Integer>();
        while (i >= 0 && ans.size() < 10) {
            if (tweets.get(i).userId == userId || users.get(userId).follows.contains(tweets.get(i).userId))
                ans.add(tweets.get(i).tweetId);
            i--;
        }
        return ans;
    }

    public void follow(int followerId, int followeeId) {
        if (!users.containsKey(followerId)) {
            users.put(followerId, new User(followerId));
        }
        if (!users.containsKey(followeeId)) {
            users.put(followeeId, new User(followeeId));
        }
        User user = users.get(followerId);
        user.follows.add(followeeId);
    }

    public void unfollow(int followerId, int followeeId) {
        if (!users.containsKey(followerId)) {
            users.put(followerId, new User(followerId));
        }
        if (!users.containsKey(followeeId)) {
            users.put(followeeId, new User(followeeId));
        }
        User user = users.get(followerId);
        user.follows.remove(followeeId);
    }
}

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter obj = new Twitter();
 * obj.postTweet(userId,tweetId);
 * List<Integer> param_2 = obj.getNewsFeed(userId);
 * obj.follow(followerId,followeeId);
 * obj.unfollow(followerId,followeeId);
 */
```

### [Find Median From Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

```java
class MedianFinder {
    PriorityQueue<Integer> MaxHeap;
    PriorityQueue<Integer> MinHeap;
    public MedianFinder() {
        MaxHeap=new PriorityQueue<>(Collections.reverseOrder());
        MinHeap=new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        MaxHeap.offer(num);
        MinHeap.offer(MaxHeap.poll());
        if(MinHeap.size()>MaxHeap.size()){
            MaxHeap.offer(MinHeap.poll());
        }
    }
    
    public double findMedian() {
        if(MaxHeap.size()>MinHeap.size()){
            return MaxHeap.peek()*1.0;
        }
        return (MaxHeap.peek()+MinHeap.peek())/2.0;
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```