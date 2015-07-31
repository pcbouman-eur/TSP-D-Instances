# TSP-D-Instances
A repository with instances for the TSP with Drones

The TSP with Drones (or TSP-D) is a variation of the classic Travelling Salesman Problem where a drone sits on top of a truck. The drone can either move with the truck, or fly somewhere. However, the drone can only cover a single node before it has to return to the truck. Coupling or decoupling happens at a node and requires both vehicles to synchronize, thus waiting can occur. 

Comments within an instances file start with /\* and end with \*/ and have to be ignore by a parser.

Currently this repository only contains Geometric Instances.

## Grammar of Geometric Instances
A Geometric instance defines a set of points in a two dimensional plane. The distance between two points is assumed to be the Euclidean distance.

The first number in an instance file defines the cost factor per unit of distance for the truck, the second number defines the cost factor per unit of distance for the drone. The third number defines the number of nodes in the file (this number includes the depot).

Following the first three numbers we have the definition of the locations. Every location definition is defined by two numbers and one identifier. The first number is the x-coordinate, the second number is the y-coordinate and the identifier specifies the name of the location.
