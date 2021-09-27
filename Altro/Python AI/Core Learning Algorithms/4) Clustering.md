Is a M.L. technique that involves the grouping of data points
- only work for a few specifics set of problems
	- when have a brench of information or features that don't have any labels or open information

- On few words, it finds clusters of like data points and location them
  - for example we can search 10 clusters, so we can get 10 group of data with similar value
### Basic algoritm  
1. : Randomly pick K points to place K centroids
2. : Assign all the data points to the centroids by distance. The closest centroid to a point is the one it is assigned to.
 3. : Average all the points belonging to each centroid to find the middle of those clusters (center of mass). Place the corresponding centroids into that position.
4. : Reassign every point once again to the closest centroid.
5. : Repeat steps 3-4 until no point changes which centroid it belongs to.

**EX**
- Red point hare data point
- blu triangle are Centroids 
 ![[Pasted image 20210716172935.png]] 
 - Now we check the distance of every point from eatch Centroids:
 
![[Pasted image 20210716173707.png]]

- after that we move Centroids in the center of mass e re-check the distance (same time)
![[Pasted image 20210716173849.png]]

- at the end, we can introduce new data point for see on witch claster it is assigned

[[5) Hidden Markov Models | Hidden Markov Models]]