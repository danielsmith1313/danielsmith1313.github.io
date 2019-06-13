## Autonomous Navigation Using Node Based Pathfinding

Source code available [here](https://github.com/danielsmith1313/nasa-ne-2019).

**Project description:** This project, funded through the NASA Nebraska Space Grant, focused on being able to program an educational GoPiGo robot
to navigate with existing GPS coordinates. The project started with self guided learning of the python programming language in order to control the
robot. After that, the project involved creating a user interface and programming obstacle avoidance as well as node based pathfinding. For the node
based pathfinding, I used Dijkstra's algorithm to find the shortest path from a theoretical starting point to an ending point.

### 1. Code examples:
Below is my second implementation of the algorithm. My first implementation was created using only broad research of the algorithm. This
implementation used that knowledge and research to improve and fix many other issues:
```python
    def algorithm(self):
        ######Djikstra's Logrithm######
        #See: https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm
        #Set all nodes distance to infinity
        unvisited = {n: math.inf for n in self.__nodes}
        #Set the starting node's distance to 0
        unvisited[self.__start] = 0
        
        #While the unvisited set contains data
        while unvisited:
            #Sets minNode to the key of the smallest distance
            minNode = min(unvisited, key = unvisited.get)
            #gets the neighbors of each point by going into the subkey and finding the values for each
            for neighborCounter in self.__neighbors[minNode].keys():
                #Sets a temporary cumulative distance
                tempDistance = unvisited[minNode] + self.__neighbors[minNode][neighborCounter]
                try:
                    #If the temp distance is less than the current distance, a shorter path has been found
                    if(tempDistance < unvisited[neighborCounter]):
                        #Set the distance of the neighbor to the new cumulative distance
                        unvisited[neighborCounter] = tempDistance
                        #Set the preview of the path
                        self.__prev[neighborCounter] = minNode
                #TODO: cleanup
                except Exception:
                    pass
            #Store the node that has been calculated
            self.__visited[minNode] = unvisited[minNode]
            #Get rid of the node that has been calculated
            unvisited.pop(minNode)
```

Below is my implementation of an obstacle avoidance program. I had written a similar program in my first year robotics class, 
and this was my attempt at converting it to python:

```python
def obstacleAvoidance(self):
        """(Run in a loop) detects when an obstacle is found"""
        
        
        
        #Get the distance each time from the distance sensor        
        self.__forwardDistance = self.__robotController.distanceSensor.getDistance()
        #Move forward
        self.__robotController.movementControl.setDirection("Forward")
        
            
        #If the reading is less then the set detection range for obstacles, stop the robot and run the avoidObstacle program
        if self.__forwardDistance <= self.__detectionRange:
            self.__robotController.movementControl.setDirection("Stop")
            self.avoidObstacle()

```


### 2. Pictures:

<img src="images/dummy_thumbnail.jpg?raw=true"/>

### 3. Challenges and Future Use of this Project

One major challenge of this project was the organization of code. Due to this being my first major independent and educational project, I did not have enough knowledge about organization of my project. Another issue with this project was that the implementation of the project did not contain any real life data due to time and budget constraints. The main goal of this project was to create a node based pathfinding system that would be used to find a safe path for a ground based vehicle along with gps and/or LIDAR. Specifically, as this was funded by NASA, this project would be useful on a foriegn planet where there would be many unknown factors that the robot would encounter.


