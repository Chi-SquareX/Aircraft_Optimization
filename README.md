# Aircraft_Optimization
The problem statement focuses on to minimizing the average weekly maintenance cost of the aircrafts to carry the Origin-Destination (OD) pairs in attached Excel file. An heuristic solution approach is implemented on the algorithm discussed in the article by C. Sriram, A. Haghani (2003).

Aircraft maintenance schedule is one of the major decisions an airline has to make during its operation. Though maintenance scheduling comes as an end-stage in an airline operation, it has the potential for cost savings. In this project, we shall consider the problem faced by an airline needing to construct a 7-day planning horizon cyclic schedule with maintenance constraints for a heterogeneous fleet of aircraft. 

Taking the assumptions listed above, the search technique is a combination of a depth-first search and random search is used for optimization. The procedure is performed for the new list of nodes and aircraft. The notebook has the code already run on Google Colab. The minimum weekly scheduled cost for the aircrafts is obtained to be 270. The image shows the final optimal weekly schedule for 25 aircrafts, where the rows are the planes and the columns are the days of the week, after 5000 iterations. 
## Assumptions taken:
1. Objective function is to minimize average weekly maintenance cost of the aircrafts to carry the Origin-Destination (OD) pairs in attached Excel file.
2. Homogeneous fleet (all aircrafts can fly all OD’s). Only domestic airline operations are considered.
3. Operation costs of aircrafts are assumed to be identical.
4. Maintenance types:
  (a) Type A: Every 4 days
  (b) There is no Maintenance type B here
5. Maintenance costs of aircrafts in all cities are listed in the Excel file attached. Unexpected maintenance requirements are not being considered.
6. To simplify the solution and reduce the possible combinations, assume that:
  (a) Only aircraft cycles of one week will be investigated.
  (b) for type A maintenance an aircraft maintenance schedule will happen twice a week.
  (c) Evaluate all pair of valid maintenance bases to find the optimum combination.
## Steps of the algorithm:
Step 0: Make a list of aircraft in any order. Make another list of nodes (cities) for any given day. Initialize a number of iterations = 1. 

Step 1: Let n - 1. 

Step 2: Pick the nth aircraft from the list of aircraft. 

Step 3: Let K = 1. 

Step 4: Pick the Kth node from the list of nodes. 

Step 5: If there are no more nodes available for the allocation in the Kth node, let K = K + 1 and go to step 4, otherwise go to step 6. 

Step 6: Do a depth-first search to find the best possible cyclic schedule for the nth aircraft. If a feasible cyclic schedule exists go to step 7, otherwise let K = K + 1, go to step 5. 

Step 7: Add the route to the schedule. Delete the arcs from the network that are assigned to the nth aircraft. 

Step 8: If n = number of aircraft,
1. reconstruct the network (in step 7 arcs are removed from the network, for the new iteration, these arcs need to be placed back in the network),
2. perturb the aircraft list randomly (construct a list by choosing each aircraft at random from the list of aircraft), 
3. perturb the node list randomly (construct a list by choosing each node at random from the list of nodes that belongs to any given day). If a feasible solution was found in the previous iterations, compare the current solution with the existing one, and if the current one has a lower objective function value save the current solution and delete the previous solution. Otherwise, let n = n + 1 and go to step 2. 

Step 9: If the number of iterations is less than the maximum number of iterations, increment the number of iterations and go to step 2, otherwise stop. In all test problems, the maximum number of iterations is set at 5000. 
