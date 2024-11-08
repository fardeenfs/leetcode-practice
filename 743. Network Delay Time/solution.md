Here is my solution for the problem: [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/)


## My Solution (with Dijkstra)

```python
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        graph = {}
        
        for time in times:
            if time[0] not in graph:
                graph[time[0]] = []
            graph[time[0]].append([time[1], time[2]])

        nodes_heap = []
        track = {}

        for i in range(1, n+1):
            if i == k:
                heappush(nodes_heap, (0, i))
                track[i] = 0
            else:
                track[i] = inf
        
        while nodes_heap:
            node_cost, node = heappop(nodes_heap)
            if node_cost == inf:
                return -1
            if node in graph:
                for neighbor in graph[node]:
                    if node_cost + neighbor[1] < track[neighbor[0]]:
                        track[neighbor[0]] = node_cost + neighbor[1]
                        heappush(nodes_heap, (node_cost + neighbor[1], neighbor[0]))

        time = max(track.values())

        if time == inf:
            return -1
        return time

```


## Another Solution (with Bellman Ford) - Slower than Dijkstra but accounts for negative weights

```python
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        distances = [inf] * n
        distances[k-1] = 0
        for i in range(n-1):
            count = 0
            for time in times:
                source = time[0] - 1
                target = time[1] - 1
                weight = time[2]
                if distances[source] + weight < distances[target]:
                    distances[target] = distances[source] + weight
                    count += 1
            if count == 0:
                break
        ans = max(distances)
        if ans == inf:
            return -1
        return ans

```