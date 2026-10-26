<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name:  DEEKSHA VICTOR SELVAKUMAR SINDHUPRIYA     </h3>
<h3>Register Number: 212225230041 </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>

``````
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

``````


<h2>PROGRAM</h2>
<pre><code>

```
from collections import defaultdict

H_dist = {}
Graph_nodes = defaultdict(list)

def aStarAlgo(start_node, stop_node):
    open_set = set([start_node])
    closed_set = set()
    g = {}
    parents = {}
    
    g[start_node] = 0
    parents[start_node] = start_node
    
    while len(open_set) > 0:
        n = None
        
        # Find node in open_set with the lowest f(n) = g(n) + h(n)
        for v in open_set:
            if n is None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v
                
        if n is None:
            print("Path does not exist!")
            return None
            
        # Reconstruct path if the destination is reached
        if n == stop_node:
            path = []
            while parents[n] != n:
                path.append(n)
                n = parents[n]
            path.append(start_node)
            path.reverse()
            print("Path found: {}".format(path))
            return path
            
        # Check neighbors of the current node
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

# --- Graph Input Parsing ---
# Input format: Enter total number of nodes and edges (e.g., "5 6")
n, e = map(int, input("Enter number of nodes and edges: ").split())

print("Enter edges format 'node1 node2 cost' (Press Enter on empty line when done):")
for _ in range(e):
    line = input().strip()
    if not line:
        break
    u, v, cost = line.split()
    cost = float(cost)
    Graph_nodes[u].append((v, cost))
    Graph_nodes[v].append((u, cost))

print("Enter heuristic values format 'node value' (Press Enter on empty line when done):")
for _ in range(n):
    line = input().strip()
    if not line:
        break
    node, h = line.split()
    H_dist[node] = float(h)

# Automatically setting start and goal based on heuristic definitions
start_node = max(H_dist, key=H_dist.get)
goal_node = min(H_dist, key=H_dist.get)

print(f"Starting Node: {start_node} -> Goal Node: {goal_node}")
aStarAlgo(start_node, goal_node)

<hr>

<h2>PROGRAM</h2>

```
          
   
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
<img width="931" height="761" alt="image" src="https://github.com/user-attachments/assets/eb3d617d-56ac-4339-8d36-d680b2f85ba3" />

Path found: ['A', 'F', 'G', 'I', 'J']


<hr>
<h2>Sample Graph II</h2>
<hr>

<img width="1560" height="1027" alt="image" src="https://github.com/user-attachments/assets/5c7afb79-7c6b-46d6-8e6f-c1b0c501bcc8" />



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
<img width="413" height="396" alt="Screenshot 2026-08-08 110533" src="https://github.com/user-attachments/assets/3f17c8bd-9c5e-4edc-9182-96611e275131" />

