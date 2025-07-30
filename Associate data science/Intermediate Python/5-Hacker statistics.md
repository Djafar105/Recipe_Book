# Hacker statistics
## Approaches to Probability: Analytical vs Simulation
When approaching probability, we often either rely on analytical mathematics (exact equations and predictions) or use simulations—commonly called *hacker statistics*—which involve repeated random sampling to estimate outcomes.
***
## Generating Random Numbers in Python with NumPy
In Python, we can generate random floats using `numpy.random.rand()`, which returns values in the interval `[0, 1)`. To ensure reproducibility, we use **seeds**. ,if we call `np.random.seed(42)` followed by `np.random.rand()`, we will get the same sequence of random numbers every time, even across separate runs.
``` python
import numpy 
numpy.random.rand() #generating a random float between 0 and 1
numpy.random.seed(156) #setting the seed here to 156
numpy.random.rand(1,5) #generating a random integer between 1 and 4
```

***
## True Randomness vs Computational Randomness
Computers can’t truly generate chaotic randomness because every step they take is deterministic. Even the idea of “pure randomness” is debated philosophically. What computers give us is a close imitation of randomness, built through algorithms designed to create sequences that look unpredictable.
***
## Pseudo-Random Number Generators (PRNGs)
PRNGs are deterministic algorithms that produce number sequences based on a starting value called a **seed**. This seed defines the entire sequence. If you set the same seed, the output will always be identical, no matter how many times or on which system the code runs.
***
## Seeds as Controlled Randomness
A seed acts like a controlled “room of randomness.” Using the same seed means stepping into the same room and seeing the same results. This behavior is not a flaw but a strength: it allows you to reproduce experiments, debug simulations, and track how randomness influenced your results, almost like having a version control system for random events.
***
## Random Walks

A **random walk** is a sequence of random steps where each step depends on the previous one, unlike a simple random list where values are independent. It’s essentially the *cumulative result* of random events. For example, starting at zero, each step could add or subtract 1, depending on a random choice.

To simulate many steps, we use a `for` loop to iteratively update the current position and store it in a list representing the path.

### Example: Simple 1D Random Walk
```python
import numpy as np

# Number of steps
n_steps = 10
# Start at position 0
position = 0
walk = [position]

# Generate the random walk
for i in range(n_steps):
    if np.random.rand() > 0.5 :
	    step = 1 
    else :
	    step =-1  # Random step +1 or -1
    position += step
    walk.append(position)

print("Random walk path:", walk)
```
***
##  Controlling Boundaries with `max()` and `min()`
When iterating or updating a variable, it's common to prevent it from going below a baseline (floor) or above a maximum limit (roof).  
- **Flooring:** Use `max()` to ensure the value never drops below a defined lower bound.  
  Example:  
  ```python
  step = max(0, step - 1)  # Ensures 'step' is at least 0
```
* ***Roofing:** Use `min()` to ensure the value never exceeds an upper bound.  
	Example:
```python
step = min(10, step + 1)  # Ensures 'step' is at most 10
```
***
## Random Walks and Multiple Universes

A single random walk is like observing one possible universe—it offers no guarantee of predicting overall chances. To extract meaningful insights or predictions, you need to simulate many independent universes (thousands or more). By these random walks, you can build a distribution of outcomes that can be analyzed for probabilities, trends, and expected behavior.
***
## Bet study : 
### core code : 
```python
all_walks = []

for i in range(5) :

    random_walk = [0]

    for x in range(100) :

        step = random_walk[-1]

        dice = np.random.randint(1,7)

        if dice <= 2:

            step = max(0, step - 1)

        elif dice <= 5:

            step = step + 1

        else:

            step = step + np.random.randint(1,7)
        if random.rand(0,1)<=0.0005 :
            step = 0

  

        random_walk.append(step)

    all_walks.append(random_walk)
```

## summary 

- **Roll the Dice**:  
  At each iteration, generate a random number between 1 and 6 using `np.random.randint(1, 7)` to simulate a dice roll.

- **Generate the Step**:  
	- implement the walk pattern: Update `step` using the last position in the current walk list (`step = random_walk[-1]`)
	* Based on the dice result:  
	  - If ≤ 2 → `step = max(0, step - 1)`) : attempt to go back one step (
	  - If 3, 4, 5 → step +=1  
	  - If 6 → step+= `np.random.randint(1, 7)`

- ** Implement Clumsiness**:  
  If some condition is met (to be defined), force `step = 0`, simulating a fall to ground zero.

- ** Append to the Ongoing Walk**:  
  Add the updated step to the current walk list: `random_walk.append(step)`

- **Build Multiple Universes**:  
  Once 100 steps are simulated, store the entire walk in a global list: `all_walks.append(random_walk)`
***
## Additional jots : 
* a chance of x % --> np.random.rand(0,1)<=0.0x : the chance is not met 
* Plotting problem  :  Transposing 
	When simulating multiple random walks in Python, we typically store each walk as a list of positions evolving over time, and gather all walks into a container list:
	
	```python
	all_walks = [walk_1, walk_2, ..., walk_n]
	```
	Here, each `walk_i` is a list of length `T` (e.g., 100 time steps). This gives us a **matrix of shape `(n_walks, T_steps)`** — rows represent individual walks, columns represent positions at a fixed time step across all walks.
	If you plot `all_walks` directly:
	```python
	plt.plot(all_walks)
	```
	matplotlib, treats the matrice as | | | | , it then tries to plot each line , meaning taking the steps(0,100) as the universal x axis and the position at each step for each walk as the y axis --> insane garbage piece of visualisation 
	
	-->solution we transpose the matrice to accomodate the needs of matplotlib 
	```python
	np.transpose(np.array(all_walks))
```