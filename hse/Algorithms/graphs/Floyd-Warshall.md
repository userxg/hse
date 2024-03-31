multi-source algorithm
idea: take u and v and compute all `d[u][v]` via some another vertex and keep shortest
something pre computed

```
G = Adj matrix
Floyd_Warshall(G, w)
make G.matrix -> infinity where not ways
n = G.size()
for via = 0 to n - 1 (where via is vertex)
	for i = 0 to n - 1
		for j = 0 to n - 1             //go via every time
			d[i][j] = min{d[i][j](via), d[i][via] + d[via][j]}
```
 

 ![[Pasted image 20240317195544.png|500]]
 **Detect neg cycles** - negative cycles give negatives on the diagonal
  