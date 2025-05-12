# Genetic-Algorithm

1. GET USER INPUT
   Ask for number of cities (N)
   Create N×N distance matrix
   For each city pair (i,j) where i < j:
       Ask for distance between them
       Set distance_matrix[i][j] = distance_matrix[j][i] = distance
   Set all diagonal distances to 0

2. INITIALIZE POPULATION
   Create empty population of size P
   For each individual in population:
       Create random path [0,1,2,...,N-1]
       Shuffle the path
       Calculate path distance
       Set fitness = 1 / distance

3. RUN GENERATIONS
   For G generations:
       a. SELECT PARENTS
          Keep top E individuals unchanged (elitism)
          For remaining individuals:
              Pick T random individuals
              Select the fittest as parent1
              Repeat to select parent2
              
       b. CREATE CHILDREN
          With probability C:
              Do ordered crossover:
                  Pick random segment from parent1
                  Fill remaining cities in order from parent2
          Otherwise:
              Copy selected parent
              
       c. APPLY MUTATION
          With probability M:
              Pick two random positions
              Reverse the path segment between them
              Update distance and fitness
              
       d. REPORT PROGRESS
          Every 50 generations:
              Print best distance so far

4. SHOW RESULTS
   Print best path found
   Print its total distance
   Print path as city sequence (starting and ending at first city)

KEY FUNCTIONS:

CALCULATE_DISTANCE(path):
   total = 0
   For each consecutive city pair in path:
       total += distance between them
   Add distance from last back to first city
   Return total

ORDERED_CROSSOVER(p1, p2):
   child = empty path
   Pick random start and end points
   Copy p1's segment to child
   Fill remaining spots with p2's cities in order, skipping duplicates
   Return child

INVERSION_MUTATION(path):
   Pick two random positions
   Reverse the segment between them
   Return mutated path
