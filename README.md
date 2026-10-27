# Assignment 3 — Maze Escape

**Course:** Design and Analysis of Algorithms  
**Student:** Nurkhan Karashev  
**Student ID:** 254828
**Language:** Java 17

## Project Description

This project is about creating a maze and finding a path to the exit.

I used DSU, Kruskal, Prim, DFS and Kosaraju algorithms. The program also finds the fastest route between zones.

## Program Output

```text
Broken: 71
Kept: 56
Last broken wall: 96
MST cost: 21998
Heaviest broken wall: 738
Path length: 21
DFS visited: 64
Dead ends: 23
Zones: 9
Largest zone: 15
Is DAG: 0
Flow stages: 6
Fastest route cost: 22
```

## Mission 0 — Disjoint Set Union

I created the DisjointSet class with four methods:

- find() finds the root of a set.
- union() joins two sets.
- connected() checks if two elements are in the same set.
- count() returns the number of sets.

I used path compression and union by size to make the operations faster.

I also added tests in DisjointSetTest.java.

## Mission 1 — Build the Maze

I used DSU to build the maze.

The program reads walls in file order. It breaks a wall if it connects two different groups.

**Why is Broken always R*C - 1?**

There are R*C cells. To connect all cells without cycles, we need exactly R*C - 1 connections.

**Why is Kept always (R-1)*(C-1)?**

The total number of inner walls is R*(C-1) + C*(R-1).

After breaking R*C - 1 walls, the number of remaining walls is (R-1)*(C-1).

## Mission 2 — Cheapest Maze

I used Kruskal and Prim to find the minimum spanning tree.

Kruskal sorts walls by cost and chooses the cheapest walls without creating cycles.

Prim starts from one cell and adds the cheapest connection to a new cell.

Both algorithms return the same minimum total cost.

My MST cost is 21998.

## Mission 3 — Escape

I used DFS to find a path from the start to the exit.

DFS uses a stack instead of recursion to avoid stack overflow on large mazes.

**Why is there exactly one path?**

The maze is a tree. It connects every cell and has no cycles. In a tree, there is exactly one path between any two cells.

My path length is 21.

## Mission 4 — Zones

I used Kosaraju to find strongly connected components.

Each zone contains cells that can reach each other using slides.

**Why do we use the reversed graph?**

The first DFS finds the finishing order. The second DFS uses reversed edges to find the cells belonging to each strongly connected component.

**Why is Zones equal to the number of cells when there are no cycles?**

Without cycles, each cell forms its own zone. If a graph has a cycle, the cells on that cycle belong to the same zone.

My program found 9 zones.

## Mission 5 — Fastest Route

I created a graph where each vertex represents a zone.

I used the topological order of zones to find the cheapest route from the start to the exit.

**Why is this order enough?**

The graph of zones has no cycles. We can process each zone once in topological order and update the costs of the next zones.

The algorithm takes O(Z + S) time, where Z is the number of zones and S is the number of slides.

My fastest route cost is 22.

## Mission 6 — Git

I used Git to save my project changes.

I created commits for my work and used GitHub to store the project.

## Mission 7 — Picture and Timing

The program creates two files:

- output/maze.png
- output/maze.html

The HTML page shows the maze and allows movement using arrow keys.

### Benchmark Results

Run `java -cp out Bench` and enter the average times from your computer.

| Maze size | Kruskal (ms) | Prim (ms) |
|---|---|---|
| 100×100 | TODO | TODO |
| 300×300 | TODO | TODO |
| 1000×1000 | TODO | TODO |

Both algorithms take more time when the maze gets bigger.
For 100x100 and 300x300, Prim was faster.
For 1000x1000, Kruskal was faster.

Both algorithms take more time when the maze becomes larger because they need to process more cells and walls.

### Time and Space Complexity

| Algorithm | Time | Space |
|---|---|---|
| DSU | O(α(V)) amortized | O(V) |
| Kruskal | O(E log E) | O(V + E) |
| Prim | O(E log V) | O(V + E) |
| DFS | O(V + E) | O(V) |
| Kosaraju | O(V + E) | O(V + E) |
| Fastest route | O(Z + S) | O(Z + S) |

V = number of vertices  
E = number of edges  
Z = number of zones  
S = number of slides

## Testing

I checked my program using:

```bash
javac -d out src/*.java
java -cp out DisjointSetTest
java tools/Check.java
java -cp out Main
```

All DSU checks passed.

The tiny, small and dag examples passed all 13 output checks.
### Additional Checks

I added more tests for the DisjointSet class.

The new tests check the number of sets, joining
two elements, checking connections, and preventing
duplicate unions.

These tests help me check that DSU works correctly.

## AI Use

I used ChatGPT to understand the assignment, explain algorithms, review errors and help prepare this README. I checked the program using the provided tests.

## Conclusion

In this project, I learned how to use graph algorithms to build a maze and find paths. I also practiced Java, testing and Git.