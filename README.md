<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Thanks again! Now go create something AMAZING! :D
-->



<!--  -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
<!--
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
-->


<!-- PROJECT LOGO -->
<br />
<p align="center">
  </a>


  <h1 align="center">Sliding Puzzle Solver</h1>


  <p align="center">
    Optimalcpp-based solver of Sliding Block Puzzle game in C++ using concepts of Graph Theory.
  </p>
</p>

![Screenshot (206)](https://user-images.githubusercontent.com/75406889/124659349-7b626600-dec2-11eb-9fcb-c09fab1ac6fa.png)

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
    </li>
    <li>
      <a href="#checksolvablecpp">CheckSolvable.cpp</a>
    </li>
    <li>
      <a href="#puzzlestatecpp">PuzzleState.cpp</a>
    </li> 
    <li>
      <a href="#bfscpp">BFS.cpp</a>
    </li>
    <li>
      <a href="#astarcpp">A_Star.cpp</a>
    </li>
    <li>
      <a href="#idastarcpp">IDA_Star.cpp</a>
    </li>
    <li>
      <a href="#visualization-of-output">Visualization of Output</a>
    </li>
    <li>
      <a href="#conclusion">Conclusion</a>
    </li>
    <!--
    <li><a href="#acknowledgements">Acknowledgements</a></li>
    -->
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

This is a N^N Sliding Puzzle game solver in CPP. Various graph traversal and shortest path algorithms like Breadth First Search , A Star and Iterative Deepening A Star are used to solve the N^N puzzle board.

## CheckSolvable.cpp
All instances of a sliding puzzle is not solvable. This function checks if the given instance of puzzle board is solvable or not :
1. If N is odd, then puzzle instance is solvable if number of inversions is even in the input state.
2. If N is even, puzzle instance is solvable if 
 - the blank is on an even row counting from the bottom (second-last, fourth-last, etc.) and number of inversions is odd.
 - the blank is on an odd row counting from the bottom (last, third-last, fifth-last, etc.) and number of inversions is even.
For all other cases, the puzzle instance is not solvable.

Inversion Count of a puzzle state : If we consider the board to be a single dimensional array , then inversion count is the number of tile pairs (a,b) where a<b , but index of a is more than index of b.


<!--PriceTracker.py-->
## PuzzleState.cpp
This puzzle is represented as a graph where each state of board corresponds to a different vertex and each valid movement of the blank tile (by swapping with any top , bottom , left or right tile) represents the graph edges. This file also prints the solution moves obtained from the puzzle solver. For each current state , the parent state is also present. 

Two heuristics are also maintained here : Manhattan Distance Heuristics and Hamming Distance Heuristics.

**Hamming Distance Heuristics** : Count the number of misplaced tiles between current state and goal state. It never overestimates the steps required to solve.

**Manhattan Distance Heuristics** : Sum of manhattan distances of all the numbered tiles between the current and goal state. This is a better heuritic function that reaches goal state quickly.

Also this file contains the function to backtrack and print the moves via which the puzzle state gets solved.

## BFS.cpp

This file solves the puzzle using Breadth First Search algorithm. This follows brute force approach to reach the target state. Maintains a visited list of states to avoid visiting the same state again. Since it is a shortest path based algo , the solution state nearest to the root is always found. But it is not so efficient in terms of memory and time usage and ends up taking the same number of moves as Depth First Search.

## A_Star.cpp

Here, the puzzle is solved using the A_star algorithm, which turns out to be the fastest solver. Here each move is always made to the state with the least cost. This approximate cost F(x) is calculated as: **F(x) = g(x) + h(x)** where, g(x) gives the number of moves from the root to the current state, while h(x) is a heuristics function. 
Two types of heuristics are used here, Hamming distance and Manhattan Distance Heuristics, which intelligently underestimates the moves required to reach the goal state. In this way, it avoids searching subtrees that do not contain an answer, and only explores sub-trees with the least cost.

## IDA_Star.cpp

This file solves the puzzle using the Iterative Deepening A Star algorithm, which is a variant of Iterative Deepening Depth First Search and A Star. This puzzle solver is the memory-efficient variant of the above algorithms, because it does not maintain a list of visited states (like the memoization of dynamic programming used by A Star), and may end up visiting the same states again. Because heuristics is used to calculate the approximate cost of each state, it doesn't search for the goal state in subtrees that do not contain a solution state. Also in the worst case, the nodes with smaller depth (i.e. the nodes without more branching & depth) are visited more than once.

## Visualization of Output

Initial State<br/>
[3 8 5]<br/>
[0 7 1]<br/>
[2 6 4]<br/>

![Screenshot (198)](https://user-images.githubusercontent.com/62290422/124349490-e1be5e80-dc0c-11eb-8cef-4fc6e1d4b062.png)

![Screenshot (200)](https://user-images.githubusercontent.com/62290422/124349497-e84cd600-dc0c-11eb-97e3-b2f7197002a0.png)

## Conclusion

**BFS :** took **23** steps . Time taken to execute: **4.646 s**

**A Star :** took **23** steps . Time taken to execute: **0.07 s**

**IDA Star :** took **25** steps . Time taken to execute: **1.598 s**








