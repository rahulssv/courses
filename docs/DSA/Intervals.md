# Intervals

### [Insert Interval](https://leetcode.com/problems/insert-interval/)

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        
        List<int[]> result = new ArrayList<>();
        
        // Iterate through all slots
        for(int[] slot : intervals)
        {
            
            // if newInterval before slot insert newInterval & update slot as new interval
            if(newInterval[1] < slot[0])
            {
                result.add(newInterval);
                newInterval = slot;
            } 
            
            // if slot is lesser than new Interval insert slot
            else if(slot[1] < newInterval[0])
            {
                result.add(slot);
            } 
            
            // if above conditions fail its an overlap since possibility of new interval existing in left & right of slot is checked
            // update lowest of start & highest of end & not insert
            else {
                newInterval[0] = Math.min(newInterval[0],slot[0]);
                newInterval[1] = Math.max(newInterval[1],slot[1]);
            }
        }
        
        // insert the last newInterval
        result.add(newInterval);
        
        // convert to int[][] array
        return result.toArray(new int[result.size()][]);
    }
}
```

### [Merge Intervals](https://leetcode.com/problems/merge-intervals/)

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals.length <= 1) {
			return intervals;
        }
        
        Arrays.sort(intervals, (a, b) -> (a[0] - b[0]));
        
        List<int[]> result = new ArrayList<>();
		for (int[] interval : intervals) {
            // if list is empty or does not overlap with the previous, just append
            if (result.isEmpty() || result.get(result.size() - 1)[1] < interval[0]) {
                result.add(interval);
            } else {
                // if overlap, merge the current and previous intervals
                result.get(result.size() - 1)[1] = Math.max(result.get(result.size() - 1)[1], interval[1]);
            }
		}

		return result.toArray(new int[result.size()][]);
    }
}
```

### [Non Overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

Actually, the problem is the same as "Given a collection of intervals, find the maximum number of intervals that are non-overlapping." (the classic Greedy problem: [Interval Scheduling](https://en.wikipedia.org/wiki/Interval_scheduling#Interval_Scheduling_Maximization)). With the solution to that problem, guess how do we get the minimum number of intervals to remove? : )

Sorting Interval.end in ascending order is O(nlogn), then traverse intervals array to get the maximum number of non-overlapping intervals is O(n). Total is O(nlogn).

```java
    public int eraseOverlapIntervals(Interval[] intervals) {
        if (intervals.length == 0)  return 0;

        Arrays.sort(intervals, new myComparator());
        int end = intervals[0].end;
        int count = 1;        

        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i].start >= end) {
                end = intervals[i].end;
                count++;
            }
        }
        return intervals.length - count;
    }
    
    class myComparator implements Comparator<Interval> {
        public int compare(Interval a, Interval b) {
            return a.end - b.end;
        }
    }
```

### [Meeting Rooms](https://leetcode.com/problems/meeting-rooms/)

```java

```

### M[eeting Schedule](https://neetcode.io/problems/meeting-schedule)

```java

```

### [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)

```java

```

### M[eeting Schedule](https://neetcode.io/problems/meeting-schedule-ii) II

```java

```

### [Minimum Interval to Include Each Query](https://leetcode.com/problems/minimum-interval-to-include-each-query/)

Sort `queries` and intervals.

Iterate `queries` from small to big,

and find out all open intervals `[l, r]`,

and we add them to a priority queue.

Also, we need to remove all closed interval from the queue.

In the priority, we use

`[interval size, interval end] = [r-l+1, r]` as the key.

The head of the queue is the smallest interval we want to return for each query.

# **Complexity**

Time `O(nlogn + qlogq)`

Space `O(n+q)`

where `q = queries.size()`

**Java**

Using TreeMap

```java
    public int[] minInterval(int[][] A, int[] queries) {
        TreeMap<Integer, Integer> pq = new TreeMap<>();
        HashMap<Integer, Integer> res = new HashMap<>();
        int i = 0, n = A.length, m = queries.length;
        int[] Q = queries.clone(), res2 = new int[m];
        Arrays.sort(A, (a, b) -> Integer.compare(a[0] , b[0]));
        Arrays.sort(Q);
        for (int q : Q) {
            while (i < n && A[i][0] <= q) {
                int l = A[i][0], r = A[i++][1];
                pq.put(r - l + 1, r);
            }
            while (!pq.isEmpty() && pq.firstEntry().getValue() < q)
                pq.pollFirstEntry();
            res.put(q, pq.isEmpty() ? -1 : pq.firstKey());
        }
        i = 0;
        for (int q : queries)
            res2[i++] = res.get(q);
        return res2;
    }
```