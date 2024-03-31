**0-1 BFS Single Source Shortest Path Algorithm:**  
uses Double ended queue
with weight 0 push in Front
1 opposite

**Space and Time Complexity:**  
time O(V+E).
space - O(V)

This problem can also be solved by Dijkstra but the time complexity will be O(E + V Log V) whereas by BFS it will be O(V+E).
**Pseudocode (Cormen Style):**
![[Pasted image 20240321195137.png|500]]

**Explanation of Pseudocode:**  
This pseudocode outlines the 0-1 BFS algorithm where distances are initialized, the source vertex is set to distance 0, and vertices are enqueued based on edge weights to efficiently find the shortest path from the source vertex to all other vertices in the graph[