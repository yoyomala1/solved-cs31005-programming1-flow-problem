Download Link: https://assignmentchef.com/product/solved-cs31005-programming1-flow-problem
<br>
Consider a flow problem where, unlike the maximum-flow problem you have seen so far, there are no special vertices <em>s</em> (source) and <em>t</em> (sink). However, each vertex may produce some amount of an item or consume some amount of the item. In addition, the vertices allow items to flow through them for distribution to other vertices. Let <em>n</em>(<em>i</em>) denote the amount that a vertex <em>i</em> produces or consumes. Thus, if <em>n</em>(<em>i</em>) = 0, the vertex is neither a producer nor a consumer, the vertex is a consumer if <em>n</em>(<em>i</em>) &gt; 0, and the vertex is a producer if <em>n</em>(<em>i</em>) &lt; 0. The items produced are shipped along the edges to satisfy the needs of the consumers. The flow assignments along the edges should be such that in addition to the standard capacity constraints, if vertex <em>i</em> is a producer then its total outflow must be greater than its total inflow by |<em>n</em>(<em>i</em>)| at any time, if vertex <em>i</em> is a consumer then its total inflow must be greater than its total outflow by |<em>n</em>(<em>i</em>)| at any time, and the total inflow must be equal to the total outflow for all other vertices.




<strong>Your input is: </strong>




A directed graph with non-negative integral capacities on every edge, and need <em>n</em>(<em>i</em>) on every vertex <em>i</em>. The graph will be given in a file in a specific format that your program will first read into an adjacency list. You can assume that the <em>n</em>(<em>i</em>) values will be positive or negative integers or 0.




<strong>Your program should output: </strong>




An assignment of flow <em>f</em> on every edge subject to the above conditions if possible, or say that it is not possible. For example, as a trivial case, if all <em>n</em>(<em>i</em>) are positive, no flow assignment is possible satisfying the above conditions (as there are no producers for the consumers).




Your program should contain the following types/functions etc. Please adhere strictly to the type/function names, function prototypes etc. so that your program runs properly when TAs test it. Do not use the structure field names for any other variable names in your program.




<ol>

 <li>Define a C type called <strong><em>EDGE</em></strong> that represents one edge of a flow network. The structure that you typedef should store 4 fields: an integer <em>y</em> storing the endpoint vertex <em>y</em> of an edge (<em>x</em>, <em>y</em>) (edge from x to <em>y</em>), an integer <em>c</em> storing the capacity of the edge, an integer <em>f</em> storing the flow value to be assigned on the edge, and a <em>next</em> field pointing to an <strong><em>EDGE</em></strong> type node (for creating a linked list of edges).</li>

 <li>Define a C type called <strong><em>VERTEX</em></strong> to represent one vertex of the flow network. The structure that you typedef should contain 3 fields, an integer <em>x</em> storing the id of the vertex, an integer <em>n</em> storing the need value of the vertex, and a pointer <em>p</em> storing a pointer to an <strong><em>EDGE</em></strong> node (basically <em>p</em> will point to the first node in the adjacency list of the vertex).</li>

 <li>Define a C type called <strong><em>GRAPH</em></strong> that stores the directed graph. The graph will be stored as an adjacency list. The C structure that you typedef should store 3 things: an integer <em>V</em> storing the number of vertices, an integer <em>E</em> storing the number of edge, and a pointer <em>H</em> storing a pointer to an array of <strong><em>VERTEX</em></strong> nodes (basically <em>H</em> stores a pointer to an array containing the vertices of the adjacency list, with each vertex pointing to its edge list).</li>

 <li>Define a function <strong><em>GRAPH *ReadGraph(char *fname)</em></strong> that reads the graph from a file whose name is given in the null-terminated string <em>fname</em>. It should also initialize the fields appropriately. The function should return a pointer to the graph formed. The format of the input file is described at the end.</li>

 <li>Define a function <strong><em>void PrintGraph(GRAPH G)</em></strong> that prints the graph <em>G</em>. A sample format for printing the graph is described at the end.</li>

 <li>Define a function <strong><em>void ComputeMaxFlow(GRAPH *G, int s, int t)</em></strong> that takes as parameter a pointer to a graph <em>G</em>, the id of the source vertex s and the id of the sink vertex t, and computes the maximum flow on it. The function should fill up the <em>f</em> field in every edge in the graph with final flow value assigned on that edge when the maximum flow is found. In addition, it should print the value of the maximum flow with a nice message. You should use the Ford-Fulkerson method, with the constraint that at every step, you should choose the augmenting path with the maximum residual capacity among all shortest augmenting paths (i.e., find the set of all augmenting paths with smallest number of edges, and among them choose the one with the maximum residual capacity).</li>

 <li>Define a function <strong><em>void NeedBasedFlow(GRAPH *G)</em></strong> that takes as parameter a pointer to a graph <em>G</em> and computes the flow values on every edge for the need-based flow. The function should fill up the <em>f</em> field in every edge in the graph with the flow assigned on that edge. This function must call the <strong><em>ComputeMaxFlow function()</em></strong> (so you should see how you can use the max flow problem to solve this, do not design a totally different algorithm of your own for this assignment, that will not be graded).</li>

 <li>Design a main function that does the following exactly in this order:

  <ol>

   <li>Read in the file name from the keyboard into a string <em>S</em> (you can assume that the maximum size of the file name is 20 characters)</li>

   <li>Call the function <strong><em>ReadGraph()</em></strong> to read and initialize the graph</li>

   <li>Call the function <strong><em>PrintGraph()</em></strong> to print the graph</li>

   <li>Read in the identifiers of the source and the sink (in that order)</li>

   <li>Call the function <strong><em>ComputeMaxFlow()</em></strong> to compute and print the maxflow in the graph, taking the ids read in as source and sink</li>

   <li>Call the function <strong><em>PrintGraph()</em></strong> to print the graph</li>

   <li>Call the function <strong><em>ReadGraph()</em></strong> again to read and initialize the graph (as the original graph has been changed by the <em>ComputeMaxFlow()</em> call)</li>

   <li>Call the function <strong><em>NeedBasedFlow()</em></strong> to compute the need-based flow in the graph</li>

   <li>Call the function <strong><em>PrintGraph()</em></strong> to print the graph</li>

  </ol></li>

</ol>




<h1>Input File Format</h1>

If the graph has <em>N</em> vertices, the vertices will be identified by the integers 1, 2, ….,<em>N</em>.

The first line of the file contains 2 integers, <em>N</em> followed by <em>M</em> (separated by spaces), where <em>N</em> is the number of vertices and <em>M</em> is the number of edges

The second line contains <em>N</em> integers, with integer <em>i</em> representing the need value of vertex <em>i</em>.

This is followed by <em>M</em> lines, with each line containing three integers <em>x</em>, <em>y</em>, <em>c</em> separated by spaces where <em>x</em> and <em>y</em> represent the vertex identifiers of the edge from <em>x</em> to <em>y</em>, and <em>c</em> represents the capacity of the edge.

For example, consider the following graph with 3 vertices and 3 edges. The identifiers for each vertex are shown inside the circle representing the vertex, and the need of the vertex is shown against it just outside the circle.

Then the graph will be represented in the file by the following lines:

3  3

-5  5  0

1  2  7

3  1  12

2  3  10

<strong> </strong>

<h1>Output Print Format</h1>

Print the graph as a normal adjacency list in the following format, with one line for the edge list of each vertex 1, 2, 3,….,N 1 -&gt; (<em>x</em>, <em>c</em>, <em>f</em>) -&gt; (<em>x</em>, <em>c</em>, <em>f</em>)-&gt;….

2 -&gt; (<em>x</em>, <em>c</em>, <em>f</em>) -&gt; (<em>x</em>, <em>c</em>, <em>f</em>)-&gt;….

.

N -&gt; (<em>x</em>, <em>c</em>, <em>f</em>) -&gt; (<em>x</em>, <em>c</em>, <em>f</em>)-&gt;….




For example, if you want to find a need-based flow, the example graph will be printed as

1 -&gt; (2, 7, 5)

2-&gt; (3, 10, 0)

3-&gt; (1, 12, 0)

You can verify that the flow assignments satisfy the constraints of a need-based flow for the example graph shown.