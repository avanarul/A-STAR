# ExpNo 4: Implement A\* Search Algorithm for a Graph

Name: s avan arul

Register Number: 212225040036

## Aim:

To Implement A\* Search algorithm for a Graph using Python 3.

## Algorithm:

1. Initialize the open list.
2. Initialize the closed list and put the starting node on the open list (you can leave its f at zero).
3. While the open list is not empty:

   a) Find the node with the least f on the open list, call it "q".

   b) Pop q off the open list.

   c) Generate q's 8 successors and set their parents to q.

   d) For each successor:

   i) If successor is the goal, stop search.

   ii) Else, compute both g and h for successor.

   successor.g = q.g + distance between successor and q

   successor.h = distance from goal to successor (This can be done using many ways, we will discuss three heuristics - Manhattan, Diagonal and Euclidean Heuristics).

   successor.f = successor.g + successor.h

   iii) If a node with the same position as successor is in the OPEN list which has a lower f than successor, skip this successor.

   iv) If a node with the same position as successor is in the CLOSED list which has a lower f than successor, skip this successor. Otherwise, add the node to the open list.

   e) Push q on the closed list.
4. End (while loop).

## Program:

```

from collections import defaultdict

H_dist = {}

def aStarAlgo(start_node, stop_node):
    open_set = set([start_node])
    closed_set = set()
    g = {}
    parents = {}

    g[start_node] = 0
    parents[start_node] = start_node

    while len(open_set) > 0:
        n = None

        for v in open_set:
            if n is None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v

        if n is None:
            print("Path does not exist!")
            return None

        if n == stop_node:
            path = []
            while parents[n] != n:
                path.append(n)
                n = parents[n]
            path.append(start_node)
            path.reverse()
            print("Path found: {}".format(path))
            return path

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

def get_neighbors(v):
    return Graph_nodes.get(v, [])

def heuristic(n):
    return H_dist.get(n, 0)

graph = defaultdict(list)

n, e = map(int, input().split())

for _ in range(e):
    line = input().strip()
    u = line[0]
    v = line[1]
    cost = float(line[2:])
    graph[u].append((v, cost))
    graph[v].append((u, cost))

for _ in range(n):
    node, h = input().split()
    H_dist[node] = float(h)

Graph_nodes = graph

start_node = max(H_dist, key=H_dist.get)
goal_node = min(H_dist, key=H_dist.get)

aStarAlgo(start_node, goal_node)


```

## Sample Graph I

### Sample Input

```
10 14
AB6
AF3
BD2
BC3
CD1
CE5
DE8
EI5
EJ5
FG1
GI3
IJ3
FH7
IH2
A 10
B 8
C 5
D 7
E 3
F 6
G 5
H 3
I 1
J 0
```

### Sample Output

The PDF does not provide readable output text for this sample.

## Sample Graph II

### Sample Input

```
6 6
AB2
BC1
AE3
BG9
ED6
DG1
A 11
B 6
C 99
E 7
D 1
G 0
```

### Output
<img width="907" height="827" alt="Screenshot 2026-10-31 133734" src="https://github.com/user-attachments/assets/1bc2d598-2587-48f9-a97d-a40bb8b2a005" />
<img width="787" height="720" alt="Screenshot 2026-10-31 133753" src="https://github.com/user-attachments/assets/c3a4db15-32f3-4298-a7c9-2d8faba24687" />



## Result:

The Python program to Implement A\* Search algorithm for a Graph has been executed successfully.
