# TSP-D-Instances
A repository with instances for the TSP with Drones

The TSP with Drones (or TSP-D) is a variation of the classic Travelling Salesman Problem where a drone sits on top of a truck. The drone can either move with the truck, or fly somewhere. However, the drone can only cover a single node before it has to return to the truck. Coupling or decoupling happens at a node and requires both vehicles to synchronize, thus waiting can occur. 

Comments within an instances file start with /\* and end with \*/ and have to be ignore by a parser.

Currently this repository only contains Geometric Instances.

This repository contains the instances used for the paper *Optimization Approaches for the Traveling Salesman Problem with Drone. Niels Agatz, Paul Bouman, and Marie Schmidt. Transportation Science 2018 52:4, 965-981* [https://doi.org/10.1287/trsc.2017.0791](https://doi.org/10.1287/trsc.2017.0791)

In the 1.3 version of the repository, we also added uniform instances of sizes 10 to 20 that we solved in the paper *Dynamic programming approaches for the traveling salesman problem with drone. Paul Bouman, Niels Agatz and Marie Schmidt. Networks. 2018; 72: 528– 542.* [https://doi.org/10.1002/net.21864](https://doi.org/10.1002/net.21864)

You are kindly requested to cite these papers if these instances are relevant to your research. Some relevant Java code to work with these instances can be found [in this related Github repository](https://github.com/pcbouman-eur/Drones-TSP).

## Grammar of Geometric Instances
A Geometric instance defines a set of points in a two dimensional plane. The distance between two points is assumed to be the Euclidean distance.

The first number in an instance file defines the cost factor per unit of distance for the truck, the second number defines the cost factor per unit of distance for the drone. The third number defines the number of nodes in the file (this number includes the depot).

Following the first three numbers we have the definition of the locations. Every location definition is defined by two numbers and one identifier. The first number is the x-coordinate, the second number is the y-coordinate and the identifier specifies the name of the location.

## Restricted Instances
In the `restricted` subfolder, we have instances that add certain restrictions on top of the regular geometric instances. In our paper *Optimization Approaches for the Traveling Salesman Problem with Drone*, the impact of these restrictions is investigated.

The `maxradius` restrictions imply that the drone can not fly further than a certain distance within a single operation. In the paper, this is expressed using a percentage of the maximum distance of a pair of locations in the instance. Since an operation involves two drone legs, the maximum drone radius that has to be considered in a single operation is 200% of the maximum distance between a pair of locations. The suffix `-maxradius-100.txt` indicates that the maximum drone radius in that instance was determined as 100% of the maximum distance between a pair of locations. Within the instance file itself, the maximum drone radius is indicated in absolute terms by a line that looks like `#MAXFLY 10`, which would indicate that the maximum distance the drone is allowed to fly is 10.

The `novisit` restrictions imply that certain locations can not be covered by the drone. As it matters a lot for the solution value which exact locations were indicated as non-drone locations, these locations were randomly sampled a number of times for each instance. The suffix `-novisit-20-rep_2.txt` indicates that for this instance 20% of the locations were selected to be non-drone locations and that this is the second random repition for this particular instance. Within the instance files, the precise locations are indicated by lines that look like `#NOVISIT 1`, which indicates that the second location defined in the instance can not be visited by a drone.

## Solutions to Instances
We have added some solutions for the instances. For instances up to size 7 we have provided exact solutions with the suffix `sMIP.txt`. For all instances we have also provided a TSP tour as found by the [Concorde TSP Solver](http://www.math.uwaterloo.ca/tsp/concorde.html). These solutions do not include the drone and have the suffix `tsp.txt` in their file name.

In v1.3 of this repository, we have added exact solutions for uniform instances up to size 17 based on our second paper. We also added solutions for instances up to size 20 with the additional restriction that the number of nodes visited by the truck in a single operation is restricted. For example, a solution `uniform-1-n18-lim_2-DP` is the optimal solution if we assume that each operation can have at most two truck-only nodes. However, we are not certain if there are better solutions possible if there can be more truck-only nodes in an operation.

The grammar of the solution files is relatively straightforward. Ignoring java-style comments, the first number in the file contains the number of operations to be parsed. The tour the consists of an operation. Every operation is contained on a single line. The first number is the id of the start node of the operation, the second number is the end node of the operation. The third number is the node that should be covered by the drone (or 0 if no node is to be covered by the drone in this operation). The fourth number is the number of internal nodes (those visited by the truck besides the start and end node). If this number is larger than 0, there will be that many additional node indices on this line, in the order they are visited by the truck.
