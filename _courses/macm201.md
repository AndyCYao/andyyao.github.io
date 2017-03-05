---
layout: default
title: "Discrete Math II"
code: "Macm 201"
semester: "Winter 2017"
---
### MACM 201 Discrete Math II Winter 2017

## Euler Trail and Euler Circuits
if G is a connected graph. G has a *Euler circuit* if the circuit traverses every edge of the graph exactly once.

it is a *Euler trail* if it's open and traverse every edge once. 

## Theorem -  If G=(V, E) is an undirected graph or multi graph , then sum of all the degrees of the vertices are 2|E|

Proof - 
For each edge [a, b] in grpah G, the edge countributes a count of 1 to deg(a) and deg(b) respectively.

consequently, for each edge, it contributes 2 to the sum of total degrees. 

Thus 2|E| accounts for deg(v), for all v in vertices. 

## Regular Graph
This is a graph where each vertex shares the *same* degrees. if deg(v) = k for all vertices v, then the graph is call k-regular.