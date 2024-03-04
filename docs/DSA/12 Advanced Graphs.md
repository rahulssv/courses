# 12. Advanced Graphs

### [Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)

```java
class Solution {
    public List<String> findItinerary(List<List<String>> tickets) {
        List<String> res = new ArrayList<>();
        if (tickets == null || tickets.size() == 0) {
            return res;
        }  
        Map<String, PriorityQueue<String>> map = new HashMap<>();
        for (List<String> ticket : tickets) {
            map.putIfAbsent(ticket.get(0), new PriorityQueue<>());
            map.get(ticket.get(0)).add(ticket.get(1));
        }
        dfs(map, "JFK", res);        
        return res;
    }
    
    private void dfs(Map<String, PriorityQueue<String>> map, String curAirport, List<String> res) {
        while (map.containsKey(curAirport) && !map.get(curAirport).isEmpty()) {
            dfs(map, map.get(curAirport).remove(), res);
        }
        res.add(0, curAirport);
    }
}
```

### [Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/)

```java
class Solution {
    public int minCostConnectPoints(int[][] points) {
        int n = points.length, ans = 0;
        HashSet<Integer> mst = new HashSet<>();
        mst.add(0);
        int[] dist = new int[n];
        for(int i = 1; i < n; i++) dist[i] = findDist(points, 0, i);
        while(mst.size() != n) {
            // Find the node that has shortest distance
            int next = -1;
            for(int i = 0; i < n; i++) {
                if(mst.contains(i)) continue;
                if(next == -1 || dist[next] > dist[i]) next = i;
            }
            // Put the node into the Minning Spanning Tree
            mst.add(next);
            ans += dist[next];
            // Update distance array
            for(int i = 0; i < n; i++) {
                if(!mst.contains(i)) {
                    dist[i] = Math.min(dist[i], findDist(points, i, next));
                }
            }
        }
        return ans;
    }
    private int findDist(int[][] points, int a, int b) {
        return Math.abs(points[a][0] - points[b][0]) + Math.abs(points[a][1] - points[b][1]);
    }
}
```

### [Network Delay Time](https://leetcode.com/problems/network-delay-time/)

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        Map<Integer, Map<Integer,Integer>> map = new HashMap<>();
        for(int[] time : times){
            map.putIfAbsent(time[0], new HashMap<>());
            map.get(time[0]).put(time[1], time[2]);
        }
        
        //distance, node into pq
        Queue<int[]> pq = new PriorityQueue<>((a,b) -> (a[0] - b[0]));
        
        pq.add(new int[]{0, K});
        
        boolean[] visited = new boolean[N+1];
        int res = 0;
        
        while(!pq.isEmpty()){
            int[] cur = pq.remove();
            int curNode = cur[1];
            int curDist = cur[0];
            if(visited[curNode]) continue;
            visited[curNode] = true;
            res = curDist;
            N--;
            if(map.containsKey(curNode)){
                for(int next : map.get(curNode).keySet()){
                    pq.add(new int[]{curDist + map.get(curNode).get(next), next});
                }
            }
        }
        return N == 0 ? res : -1;
            
    }
}
```

### [Swim In Rising Water](https://leetcode.com/problems/swim-in-rising-water/)

```java
// 2 ms. 99.20%
class Solution {
    int n;
    private boolean dfs(int[][] grid, int i, int j, int T, boolean[][] visited) {
        if(i < 0 || i >= n || j < 0 || j >= n || visited[i][j] || grid[i][j] > T) return false;
        visited[i][j] = true;
        if(i == n-1 && j == n-1) return true;
        return dfs(grid, i-1, j, T, visited) || dfs(grid, i+1, j, T, visited) || dfs(grid, i, j-1, T, visited) || dfs(grid, i, j+1, T, visited);
    }
    public int swimInWater(int[][] grid) {
        this.n = grid.length;
        int l = grid[0][0], r = n*n - 1;
        while(l < r) {
            int m = l + ((r-l) >> 1);
            if(dfs(grid, 0, 0, m, new boolean[n][n])) {
                r = m;
            } else {
                l = m + 1;
            }
        }
        return l;
    }
}
```

### [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/)

### F[oreign Dictionary](https://neetcode.io/problems/foreign-dictionary)

### [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

```java
// Time Complexity O(k * n) | Space Complexity O(n)
class Solution {

    public int findCheapestPrice(
        int n,
        int[][] flights,
        int src,
        int dst,
        int k
    ) {
        // initialize an array with max value of size n
        int[] prices = new int[n];
        Arrays.fill(prices, Integer.MAX_VALUE);

        // price from source to source is always 0
        prices[src] = 0;

        for (int i = 0; i <= k; i++) {
            // make a copy of prices
            int[] temp = new int[n];
            temp = Arrays.copyOf(prices, prices.length);

            // loop through flights
            for (int j = 0; j < flights.length; j++) {
                int s = flights[j][0]; // from
                int d = flights[j][1]; // to
                int p = flights[j][2]; // price

                if (prices[s] == Integer.MAX_VALUE) {
                    continue;
                }

                if (prices[s] + p < temp[d]) {
                    temp[d] = prices[s] + p;
                }
            }

            // set prices to temp
            prices = temp;
        }

        if (prices[dst] != Integer.MAX_VALUE) {
            return prices[dst];
        }

        return -1;
    }
}

```