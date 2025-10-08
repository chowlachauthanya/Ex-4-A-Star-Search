<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name:Chowla Chaithanya
<h3>Register Number:2305002004           </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>


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

## PROGRAM
```python
def a_star(start, goal, graph, h):
    open_list = [start]
    g = {start: 0}
    parent = {start: None}

    while open_list:
        n = min(open_list, key=lambda x: g[x] + h[x])
        if n == goal:
            path = []
            while n:
                path.append(n)
                n = parent[n]
            return path[::-1]

        open_list.remove(n)
        for m, cost in graph.get(n, []):
            if m not in g or g[m] > g[n] + cost:
                g[m] = g[n] + cost
                parent[m] = n
                if m not in open_list:
                    open_list.append(m)
    return None

#User Input for graph
graph = {}
h = {}

nodes = input("Enter all nodes separated by space: ").split()

for node in nodes:
    h[node] = int(input(f"Heuristic value for {node}: "))
    graph[node] = []
    n = int(input(f"How many neighbors does {node} have? "))
    for _ in range(n):
        neighbor = input("  Enter neighbor node: ")
        cost = int(input(f"  Enter cost to reach {neighbor}: "))
        graph[node].append((neighbor, cost))

start = input("Enter start node: ")
goal = input("Enter goal node: ")

path = a_star(start, goal, graph, h)
print("Path found:", path)
```

SAMPLE GRAPH I
<img width="973" height="625" alt="image" src="https://github.com/user-attachments/assets/b0469711-51c4-41c5-9a75-039e5d3a41d4" />


SAMPLE INPUT
<img width="798" height="743" alt="image" src="https://github.com/user-attachments/assets/81feb7fe-6a5b-448d-89ea-e454efc5e045" />

<hr>
Sample Output

![435098048-ac8a5725-93b0-44e9-bba7-8a32d7ee80ee](https://github.com/user-attachments/assets/23a66732-b6f5-4b74-8eae-e3e21b0f6814)




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

SAMPLE OUTPUT

![435098114-175123a9-8519-4ec4-b3f6-1151b674380d](https://github.com/user-attachments/assets/91f98b2e-c195-45de-9dbf-19bc17dbfb8f)

## RESULT
