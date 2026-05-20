<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: Sitharth B S     </h3>
<h3>Register Number: 212224110048          </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>

```
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)

```
## Program
```python
from collections import defaultdict

H_dist = {}

# Function to return neighbors and distance
def get_neighbors(v):
    if v in Graph_nodes:
        return Graph_nodes[v]
    else:
        return None


# Heuristic function
def heuristic(n):
    return H_dist[n]


# A* Algorithm
def aStarAlgo(start_node, stop_node):

    open_set = set([start_node])
    closed_set = set()

    g = {}          # Store distance from starting node
    parents = {}    # Store parent nodes

    g[start_node] = 0
    parents[start_node] = start_node

    while len(open_set) > 0:

        n = None

        # Find node with lowest f(n)
        for v in open_set:
            if n is None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v

        if n is None:
            print("Path does not exist!")
            return None

        # If destination reached
        if n == stop_node:
            path = []

            while parents[n] != n:
                path.append(n)
                n = parents[n]

            path.append(start_node)
            path.reverse()

            print("Path found:", path)
            return path

        # Process neighbors
        for (m, weight) in get_neighbors(n):

            if m not in open_set and m not in closed_set:
                open_set.add(m)
                parents[m] = n
                g[m] = g[n] + weight

            else:
                if g[m] > g[n] + weight:
                    g[m] = g[n] + weight
                    parents[m] = n

                    if m in closed_set:
                        closed_set.remove(m)
                        open_set.add(m)

        open_set.remove(n)
        closed_set.add(n)

    print("Path does not exist!")
    return None


# Input graph
graph = defaultdict(list)

n, e = map(int, input("Enter number of nodes and edges: ").split())

for i in range(e):
    u, v, cost = input().split()

    graph[u].append((v, float(cost)))
    graph[v].append((u, float(cost)))   # Undirected graph

# Input heuristic values
for i in range(n):
    node, h = input().split()
    H_dist[node] = float(h)

Graph_nodes = graph

print("Heuristic Values:", H_dist)
print("Graph:", dict(graph))

# Run A*
aStarAlgo('A', 'J')


```
<hr>
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>

<img width="1717" height="632" alt="Screenshot 2026-05-16 082801" src="https://github.com/user-attachments/assets/1d4688b7-5859-4bc1-b919-f71360848c83" />


Path found: ['A', 'F', 'G', 'I', 'J']

## Program
```python
from collections import defaultdict

H_dist = {}

# Function to return neighbors and distance
def get_neighbors(v):
    if v in Graph_nodes:
        return Graph_nodes[v]
    else:
        return None


# Heuristic function
def heuristic(n):
    return H_dist[n]


# A* Algorithm
def aStarAlgo(start_node, stop_node):

    open_set = set([start_node])
    closed_set = set()

    g = {}          # Store distance from starting node
    parents = {}    # Store parent nodes

    g[start_node] = 0
    parents[start_node] = start_node

    while len(open_set) > 0:

        n = None

        # Find node with lowest f(n)
        for v in open_set:
            if n is None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v

        if n is None:
            print("Path does not exist!")
            return None

        # If destination reached
        if n == stop_node:
            path = []

            while parents[n] != n:
                path.append(n)
                n = parents[n]

            path.append(start_node)
            path.reverse()

            print("Path found:", path)
            return path

        # Process neighbors
        for (m, weight) in get_neighbors(n):

            if m not in open_set and m not in closed_set:
                open_set.add(m)
                parents[m] = n
                g[m] = g[n] + weight

            else:
                if g[m] > g[n] + weight:
                    g[m] = g[n] + weight
                    parents[m] = n

                    if m in closed_set:
                        closed_set.remove(m)
                        open_set.add(m)

        open_set.remove(n)
        closed_set.add(n)

    print("Path does not exist!")
    return None


# Input graph
graph = defaultdict(list)

n, e = map(int, input("Enter number of nodes and edges: ").split())

for i in range(e):
    u, v, cost = input().split()

    graph[u].append((v, float(cost)))
    graph[v].append((u, float(cost)))   # Undirected graph

# Input heuristic values
for i in range(n):
    node, h = input().split()
    H_dist[node] = float(h)

Graph_nodes = graph

print("Heuristic Values:", H_dist)
print("Graph:", dict(graph))

# Run A*
aStarAlgo('A', 'G')



```

<hr>
<h2>Sample Graph II</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>

<img width="1727" height="377" alt="Screenshot 2026-05-16 081530" src="https://github.com/user-attachments/assets/0b2489bb-a1e5-4a0d-8da9-e67e708cec7a" />

Path found: ['A', 'E', 'D', 'G']

## Result

Implementing A * Search algorithm for a Graph using Python 3. is executed successfully.
