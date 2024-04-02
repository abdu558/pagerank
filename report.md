# Optimisation Report
## Loading the graph
I have loaded the graph using three different methods:
-   Adjacency lists using a dictionary with the value for each key represented as a list.
-   Adjacency matrix using 2D arrays with NumPy.
-   NetworkX the external module 
-   Graph class

My initial implementation used an adjacency list, where each key represents a node and the value is a list of nodes connected to the node, the average time taken was recorded in the table below. I then tried using other implementations I started with using an adjacency matrix which was implemented with numpy, this was much slower than the initial implementation and used more, so I moved on to use the Network X module which is specialised for graphs, this was much slower than both the matrix and the adjacency list implementation, so finally I test the speeds of a graph class, which had a add node and add edge methods, this was significantly slower The table below records the times taken for each implementation from fastest to slowest. The fastest way was using an adjacency list.


Each method was tested 20 times and an average was taken, with the same conditions (laptop on charge).
| Methods          | Stochastic (avg time)| Distribution (avg time)|
|------------------|----------------------|------------------------|
| Adjacency list   | 0.44                 | 0.19                   |
| Adjacency matrix | 0.52                 | 0.21                   |
| Networkx         | 0.72                 | 0.25                   |
| Graph class      | 3.24                 | 1.29                   |

To further optimise the adjacency list implementation, I used defaultdict instead of dict initialization for faster speeds, defaultdict(list) was much faster than implementing it with {}, it may be because there isn’t a need to check if an item exists as the default values are 0. I further optimised the stochastic function by using the defaultdict(int), which initlises the value keys with 0, rather than iterating on each node in the graph and adding a 0. This improved the speeds to 0.40 (stochastic) and 0.18 (distribution).

I further optimised the adjacency list, by implementing dictionary comprehensions and list comprehension that also used the sum() built-in function, which removed a for loop which. I was able to improve the speed by an average of 5% on both functions.
Avoiding attribute lookups for the random module and the collections module, improved speed by 3%. I used Windows API, to change the priority to High. This resulted in a negligible impact and only really impacted it when other tasks were running in the background. I added support for Multi-threading however this resulted in worse performance as there was more code and a external module, this may be because there was nothing else running at the same time on the laptop.

I used the cProfiler to detect which lines took the most time and I found that getting the length of the graph took a lot of time as it was being used multiple times, so calculated it once and used it multiple times in the distribution function. 

Results:
| Methods          | Stochastic | Distribution |
|------------------|------------|--------------|
| Adjacency list   | 0.35       | 0.11         |

20% improvement in stochastic and 42% improvement in distribution speed
