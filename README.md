# Navigating Urban Environments Using Rideshare Services
Our goal is to develop an algorithm that optimizes the path to take from one neighborhood to another neighborhood, depending on whether the user wants to minimize the time, distance, or cost of the rides. We also wanted to see how much information we could extrapolate, i.e. predict the sizes of the neighborhoods in the data.

Our chosen problem of finding the best path to take to go from a starting neighborhood to an ending neighborhood
is important for several reasons. Firstly, it can help in improving the efficiency of urban transportation, reducing
traffic congestion, and minimizing the time and cost of travel. Secondly, it can aid in identifying areas of the city
that are poorly connected or under-served by transportation, allowing for better planning and resource allocation.
Finally, our chosen problem is a challenging and interesting one, which requires the use of advanced algorithms and
techniques from the field of graph theory and optimization.

We chose our goal because we believe that it has the potential to make a significant impact on the lives of people
living in urban areas, especially in large and densely populated cities. Additionally, we were drawn to the technical
and intellectual challenge that this problem presents, and we believe that by working on this project, we will be able
to develop our skills and knowledge in several areas, including data analysis, algorithm design, and optimization.

# Data Set
For our project, we used ”My Uber Drives” from user Zeeshan-Ul-Hassan Usmani. The data encompassed his
Uber drives in 2016 (1,175 drives total), and it was presented as a csv with the following columns going from left to
right: start date, end date, category, start, stop, number of miles, and purpose. ”Start” and ”stop” referred to the
pickup and drop-off neighborhoods for the Uber ride. ”category” referred to the category of the trip, for example,
business, personal, etc., and ”purpose” referred to the purpose of the trip, for example, meals, errands, etc.

# Computational Overview
As per our goal, we wanted to see if we could optimize for certain key factors of an Uber ride from one destination
to another, such as time, distance, and cost.

To start, we needed to represent our data as a graph. Graphs play a central role in our project because the states
that the Uber ride data encompasses are inherently graphs - each neighborhood connects to another, and we have the
distance and time it took for each ride to connect them. Thus, we represented each unique neighborhood as a node in
the graph, and represented the aggregate of rides between two neighborhoods as a weighted link by looking at factors
such as the time, distance, and cost between the start and stop neighborhoods. We created the graph from our
data set, and we did so through the following process: we passed the data set into read csv, passed that result into
get avg times and miles, passed the result from get avg times and miles into get avg costs. We then combine those
2 dictionaries using combine dict times miles cost, and finally passed the resulting dict into our create graph function.
To get accurate and necessary data for our project, we filtered out the ”category” and ”purpose” columns from
our data set, and this can be clearly seen in the read csv function. We also noticed that some pickup and drop-off locations were unknown, so we filtered those out too.

Since there may be multiple trips with the same endpoints, we computed the average time, average cost, and
average distance for the trip, and stored them in their respective links so that every link in our graph that connects
2 neighborhoods is weighted by these averages.

Next, we wanted to optimize paths between 2 neighborhoods. We used Dijkstra’s algorithm, which was one of
the harder algorithms that we implemented. Dijkstra’s algorithm is a popular algorithm in computer science used
to solve the shortest path problem in a graph. The goal of the algorithm is to find the shortest path from a starting
node to all other nodes in the graph.

The algorithm works by maintaining a set of unvisited nodes, a set of visited nodes, and a set of tentative dis-
tances to each node. Initially, all nodes are unvisited and the distance to each node is set to infinity, except for the
starting node, which has a distance of 0.

At each step of the algorithm, the node with the smallest tentative distance is selected and marked as visited.
Then, for each of its unvisited neighbors, the algorithm calculates a tentative distance by adding the length of the
edge connecting the current node and its neighbor to the current node’s path length so far. If this tentative distance
is less than the current recorded distance to the neighbor, the neighbor’s tentative distance is updated.

The algorithm repeats this process until all nodes have been visited, and the tentative distances for all nodes
have been calculated. The resulting set of tentative distances is the shortest path from the starting node to all other
nodes in the graph. Dijkstra’s algorithm can be applied to minimize other attributes as well, and in our case, our
find best path dijsktras method can additionally minimize path based on cost or time.

We also created the 3 functions below: run find best path for time, run find best path for distance, and
run find best path for cost. These 3 functions are similar to Dijkstra in function (i.e. finds the shortest path),
but we implemented it anyway because we wanted to try multiple coding approaches to solve the same problem.
Doing so allowed us to compare the functions as well as help us in case we ran into problems implementing the
functionality we wanted using an approach.

Additionally, we wondered if we could extrapolate any conclusions about the sizes of the neighborhoods from our
ride data (i.e. predict the sizes of neighborhoods). We implemented the estimate neighborhood size method and
assigned each neighborhood’s size to their respective size attributes.

In order to visualize our results, we used the networkx and matplotlib libraries. We did this by first con-
verting our graph to a networkx graph in the convert to nx() function. This creates networkx nodes ({networkx
obj}.add node) of the neighborhood names and assigns them a size attribute based on 50 times the natural logarithm
of respective size attributes + 1. The 50 scales the nodes to make sure that they are visible, and the log keeps large
neighborhoods from completely covering the screen. If a path is passed in, we convert it to a list of sets of endpoints,
and then use {networkx obj}.add edge to add the edge with a color attribute of red and a weight attribute of the
corresponding link’s cost. If not, we render all edges as black with the respective link costs attached. Then, by using
networkx’s spring layout and draw function, we found the positions of each node and plotted them. To visualize
the graph more clearly, we changed the parameters in the draw functions to customize node sizes, node colors, font
sizes, font colors, and edge widths. Finally, we display the resulting networkx graph using matplotlib.pyplot’s show()
method.

# Instructions for Running the Project
1. Download all files.
2. Install all required libraries in requirements.txt
3. Install the required data set zip file, extract all, and create a folder called ’data’ to store it in.
4. Make sure that the ’data’ folder is at the same depth as the other python files downloaded from the repository.
2
