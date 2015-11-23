# TSP-D-Instances
A repository with instances for the TSP with Drones

The TSP with Drones (or TSP-D) is a variation of the classic Travelling Salesman Problem where a drone sits on top of a truck. The drone can either move with the truck, or fly somewhere. However, the drone can only cover a single node before it has to return to the truck. Coupling or decoupling happens at a node and requires both vehicles to synchronize, thus waiting can occur. 

Comments within an instances file start with /\* and end with \*/ and have to be ignore by a parser.

Currently this repository only contains Geometric Instances.

## Grammar of Geometric Instances
A Geometric instance defines a set of points in a two dimensional plane. The distance between two points is assumed to be the Euclidean distance.

The first number in an instance file defines the cost factor per unit of distance for the truck, the second number defines the cost factor per unit of distance for the drone. The third number defines the number of nodes in the file (this number includes the depot).

Following the first three numbers we have the definition of the locations. Every location definition is defined by two numbers and one identifier. The first number is the x-coordinate, the second number is the y-coordinate and the identifier specifies the name of the location.

## Solutions to Instances
We have added some solutions for the instances. For instances up to size 7 we have provided exact solutions with the suffix `sMIP.txt`. For all instances we have also provided a TSP tour as found by the [Concorde TSP Solver](http://www.math.uwaterloo.ca/tsp/concorde.html). These solutions do not include the drone and have the suffix `tsp.txt` in their file name.

The grammar of the solution files is relatively straightforward. Ignoring java-style comments, the first number in the file contains the number of operations to be parsed. The tour the consists of an operation. Every operation is contained on a single line. The first number is the id of the start node of the operation, the second number is the end node of the operation. The third number is the node that should be covered by the drone (or 0 if no node is to be covered by the drone in this operation). The fourth number is the number of internal nodes (those visited by the truck besides the start and end node). If this number is larger than 0, there will be that many additional node indices on this line, in the order they are visited by the truck.
