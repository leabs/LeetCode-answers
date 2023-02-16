---
layout: post
title: 2477. Minimum Fuel Cost to Report to the Capital
date: 2023-02-12 09:52 -0500
difficulty: medium
comments: true
---

There is a tree (i.e., a connected, undirected graph with no cycles) structure country network consisting of n cities numbered from 0 to n - 1 and exactly n - 1 roads. The capital city is city 0. You are given a 2D integer array roads where roads[i] = [ai, bi] denotes that there exists a bidirectional road connecting cities ai and bi.

There is a meeting for the representatives of each city. The meeting is in the capital city.

There is a car in each city. You are given an integer seats that indicates the number of seats in each car.

A representative can use the car in their city to travel or change the car and ride with another representative. The cost of traveling between two cities is one liter of fuel.

Return the minimum number of liters of fuel to reach the capital city.

## Example

```javascript
Input: roads = [[0,1],[0,2],[0,3]], seats = 5
Output: 3
Explanation:

- Representative1 goes directly to the capital with 1 liter of fuel.
- Representative2 goes directly to the capital with 1 liter of fuel.
- Representative3 goes directly to the capital with 1 liter of fuel.
  It costs 3 liters of fuel at minimum.
  It can be proven that 3 is the minimum number of liters of fuel needed.
```

```javascript
/**
 * @param {number[][]} roads
 * @param {number} seats
 * @return {number}
 */
var minimumFuelCost = function (roads, seats) {
  const adjList = createAdjacencyList(roads);
  let ans = 0;

  const dfs = (curNode, preNode) => {
    let people = 1;
    // Traverse the children of the current node
    for (let child of adjList[curNode]) {
      // If the child is not the parent of the current node
      if (child !== preNode) {
        // Traverse the subtree of the child
        people += dfs(child, curNode);
      }
    }
    // If the current node is not the root node
    if (curNode) ans += Math.ceil(people / seats);

    return people;
  };
  dfs(0, -1);

  return ans;
};

const createAdjacencyList = (edges) => {
  // Create an empty adjacency list
  const N = edges.length;
  // Create an empty adjacency list
  const adjList = Array(N + 1)
    .fill()
    .map(() => []);

  // Add the edges to the adjacency list
  for (const edge of edges) {
    // Add the edge to the adjacency list
    const [node1, node2] = edge;
    // Add the edge to the adjacency list
    adjList[node1].push(node2);
    // Add the edge to the adjacency list
    adjList[node2].push(node1);
  }
  // Return the adjacency list
  return adjList;
};
```
