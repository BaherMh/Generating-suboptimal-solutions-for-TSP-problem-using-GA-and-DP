# Generating-suboptimal-solutions-for-TSP-problem-using-Genetic-algorithms-and-Dynamic-Programming
This work presents a combination of Genetic Algorithm (GA) with Dynamic Programming (DP) to generate suboptimal solutions to the well-known Travelling Salesman Problem (TSP). In this work, DP is integrated as a GA operator with a certain probability. In specific, at a given GA generation, the individuals are subdivided into a number of equal segments of genes, and the shortest path on each segment is obtained by applying a DP algorithm. Since the computational complexity of the DP is O($K^2*2^k$), it can be done on small segments. Experimental analyses are conducted to investigate the impact and trade-offs among DP probability, segment size and time processing on the solution quality and computational effort. In addition, we implemented a basic GA approach to compare results and show the contribution of combination approach.

# Introduction
TSP is stated as following: Let 1,2,…,n be the labels of the n cities and C = [c_(i,j)] be an n x n cost matrix where  [c_(i,j)] denotes the cost of traveling from city i to city j. TSP is the problem of finding the n-city closed tour having the minimum cost such that each city is visited exactly once. The total cost A of a tour is: A(n) = '''\sum_{i=0}^{n-1} c_{i,i+1} + c_{n,1}'''
TSP is formulated as finding a permutation of n cities, which has the minimum cost. This problem is known to be NP-hard. Many algorithms have been proposed to solve this problem. There are two main approaches for solving TSP: exact and approximate. Exact approaches are usually based on Dynamic Programming, Branch and Bound …and all gave the optimal solutions for TSP. However, the algorithms basing on these approaches have exponential running time, Dynamic Programming takes O(K^2*2^k) running time. Hence, they can only solve TSP with small number of the vertices as algorithms using branch and bound method are only able to give solutions for 40 – 60 cities set. In an attempt to solve larger instances, especially in such the NP-hard problem, researchers have concerned approximation approaches in recent years. Many approximation approaches were proposed for solving TSP such as 2- opt, 3-opt, simulated annealing, tabu search nature-based optimization algorithms and population-based optimization algorithms: genetic algorithm, evolutionary computation, neural networks, DNA computing, swarm optimization algorithms, ant colony optimization, bee colony optimization. The algorithms basing on these approaches can solve large instances and give approximate solutions near to the optimal solution within reasonable time.
In addition to above original approximation approaches, there is a different one combining exact methods with approximate methods, called Hybrid methods, tends to make exact methods make local decisions to support approximation methods which combine these solutions into a global solution.

We are going to discuss two approaches, the first of which is using genetic algorithm, and the second one is enhancing the basic genetic algorithm using DP with bitmasks optimization and compare the results.
#First Approach (basic Genetic)
1. Initialization: Create an initial population of candidate solutions. Each solution should be a permutation of the cities to be visited.
2. Evaluation: Evaluate the fitness of each candidate solution. In the context of the TSP, the fitness of a solution can be defined as the total distance traveled in the solution.
3. Selection: Select a subset of the candidate solutions to be parents for the next generation. This can be done using various selection techniques, such as tournament selection or roulette-wheel selection.
4. Crossover: 
Select two parent solutions at random.
Choose two crossover points at random.
Copy the subset of cities between the two crossover points from the first parent to the offspring.
For each city in the subset copied from the first parent, find its corresponding city in the second parent (i.e., the city that occupies the same position in the second parent).
If the corresponding city is not in the subset copied from the first parent, map the corresponding city onto the offspring by swapping it with the city that occupies the same position in the offspring.
5. Mutation: Introduce random changes to the candidate solutions to maintain diversity in the population. This can involve swapping two cities in a solution or reversing a segment of the solution.
6. Replacement: Replace the old population with the new population of candidate solutions.
7. Repeat: Repeat steps 2-6 for a fixed number of generations or until a satisfactory solution is found.
8. Termination: Return the best candidate solution found during the optimization process.

#Second Approach (Genetic + DP)
we integrate DP as a GA operator with specific probability $p_dp$. Exactly like crossover and mutation operators. This new phase will be added just before evaluation phase and after the mutation.
consists to subdivide the individual on equal segments sized k,k=5 for example, and applying DP to compute the shortest path of each segment.
