
In mathematics, a graph is a collection of nodes[^1] linked by a collection of edges[^2] .
The nodes are typically used to represent the things that the graph is about, while the edges represent how those things relate to one-another.
Edges can be undirected or directed.
Directed edges strongly distinguish between an edge $\langle a, b \rangle$ and $\langle b, a \rangle$, where as an undirected graph treats these two as equivalent.
There is a  large field of mathematics that studies graphs, their topologies, and graph functions that transform nodes, edges and entire graphs, as well as their statistical properties.

Nodes can be labelled, so that they carry additional information.
So can the edges.
For example, a social network graph may have individual people as nodes, labelled with their date of birth, email address, social media accounts and so on.
Edges represent interactions between those people, such as being friends, reading each-other's posts, membership of the same forums.

The collatz function *induces*[^3] a graph over the natural numbers, where the nodes are the numbers and the edges link a number to the value of the collatz function for that number.
This is the collatz graph.
We can label the edges by if the collatz function went down the even or odd case.
In fact, our collatz sequences with green and grey arrows is a way of displaying a sub-graph starting at some $n$ and going to 1.
It is a fairly boring, linear type of graph.
But we can look at much more interesting subsets of the collatz graph by overlaying the collatz sequence for choices of $n$ starting at 1 and going up to some upper bound.

```python
import networkx as nx
import matplotlib.pyplot as plt

def collatz(n):
	if n % 2 == 0:
		return n//2
	else:
		return 3*n+1

nodes = []
edges = []

for n in range(1, 100):
	print(n)
	while True:
		if n in nodes:
			println()
			break
		m = collatz(n)
		edges.append((n, m))
		n = m

G = nx.Graph()
G.add_edges_from(edges)
nx.draw_networkx(G)
plt.show()
```

[^1]: A node is also sometimes called a vertex.
[^2]: There is no alternative name for an edge, although they are sometimes called links.
[^3]: Something is induced, if by existing it in some sense makes something else exist.