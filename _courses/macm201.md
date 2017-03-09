---
layout: default
title: "Discrete Math II"
code: "Macm 201"
semester: "Winter 2017"
---
## MACM 201 Discrete Math II Winter 2017


### Find unique solution to a given recurrence
Given \$$ a_{n+1} - 1.5a_n = 0$$

Rearrange equation so \$$ a_{n+1} = 1.5a_n$$

then we can see that \$$ a_{n+2} = 1.5a_{n+1} = 1.5 * 1.5 * a_{n}$$

so the unique solution is \$$ a_{n} = 1.5^n * a_0 $$

### Solve a recurrence using characteristic polynomial
Given an equation such as \$$ a_n = 2a_{n-1} + 3a_{n} \quad a_0 = 1 \quad a_1 = 2 $$

Substitute \$$ a_n = cr^n $$

so the equation becomes \$$ cr^n = 2cr^{n-1} + 3cr^{n-2} $$

the key part is to divide both sides by \$$ cr^{n - lowest exponent} $$ 

in this case its 2, it becomes \$$ r^2 - 2r - 3 = 0 $$ 

move terms to one side rearrange and find the root \$$ (r+1)(r-3) = 0 $$

with r = -1 and r = 3, general equation for second order homogenous solution is \$$ a_n=A3^n+B(-1)^n $$

solve for A and B by using initial information \$$ a_1 = 1 \quad a_0 = 0 $$ 

we get 
$$ A = 3/4 \quad B=1/4 $$

The solution is thus 
$$ a_n = 3/4*3^n + 1/4*(-1)^{n} $$

### What is a graph
graph is a collection of vertices, V, and edges E. 

### Traversal terms
- Cycle is a closed Path, a Path has no repeat vertices 
- Circuit is a closed Trail, a Trail has no repeat edges
- Walk is the most general case, no restrictions. 


### Euler Trail and Euler Circuits
if G is a connected graph. G has a *Euler circuit* if the circuit traverses every edge of the graph exactly once.

it's a *Euler trail* if it's open and traverse every edge once. 

### Theorem -  If G=(V, E) is an undirected graph or multi graph , then sum of all the degrees of the vertices are 2|E|

Proof - 
For each edge [a, b] in graph G, the edge countributes a count of 1 to deg(a) and deg(b) respectively.

consequently, for each edge, it contributes 2 to the sum of total degrees. 
Thus 2|E| accounts for deg(v), for all v in vertices. 

### Regular Graph
This is a graph where each vertex shares the *same* degrees. if deg(v) = k for all vertices v, then the graph is call k-regular.

### Isomorphic,
If two graphs G1, and G2 are isomorphic, then there is a function f that is bijective, and f maps an edge E1 to E2. 

## Graph Proofs

### Proof for all x - y walks in a graph, there exists a x -y path
1. Define a w to be a minimal walk from x - y, so it is also the shortest. 

2. theres two cases for w . A.) either w has a repeated vertex, or B.) it does not.

3. for case 
  - A. Since there is a repeated vertex, call v1. this means this walk looks something like this . x - a - b - c -v1 - d -v1 - y. This means we can remove occurences of v1 so that only one v1 remains. This new walk w1 is now a path. 
  - B. we are done, as by definition it is also a path.

### Proof if graph G has a total number of vertices v. and total number of edges e. and G is loop free, undirected . prove that 2e <= v^2 - v
the key is to note that the maximum edges a graph can have is given by the complete graph of vertices v. ie. (v, 2) edges.

then its a matter of rearranging the formula of (v,2) to get v(v-1)/2

### General notes on graph proofs
We should remember the property Sum of all degrees = 2 * total edges of a graph. 

a k+1 regular graph would also have the properties of a k regular graph. 
	so if k regular graph has a k walk, the k+1 graph would also have it. 

in a induction proof, when we have establish a base case, an induction hypothesis, and we are proofing for n+1, it may be sufficient to just draw a graph n abstractly, namely, we dont care about whether its bipartite, complete, or whatever. 
