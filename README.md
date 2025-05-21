# The Goblet of Fire
## Assumptions:

+ The maze is static and its structure does not change between episodes.

+ For the first 500 episodes, the Cup is placed at a fixed position to help the agent learn basic navigation; after that, the Cup is randomly placed at the start of each episode as mentioned in the task.

+ The Death Eater always moves optimally (shortest path) toward Harry.

## Overview:
### _State Representation:_
The state includes Harry's position, the Death Eater's position, and the Cup's position. To reduce state space, relative directions (just quadrant wise) between Harry, the Cup, and the Death Eater are used.

### _Reward Shaping:_
The agent receives a large positive reward for reaching the Cup, a large negative reward for being caught, small negative step penalties, and additional shaping rewards based on proximity to the Cup and revisiting cells.

### _Environment and Algorithm Implementation:_
Maze Environment:
+ 2d grid with Harry (blue H), the Cup (yellow), and the Death Eater (red circle).
+ The Death Eater uses BFS to move optimally toward Harry.

Q-learning Agent:
+ Maintains a Q-table with keys based on state (relative positions/directions) and action.
+ Uses epsilon-greedy exploration with decaying epsilon.
+ Supports experience replay for improved learning stability.
+ The Q-table is saved to q_table.pkl after training for later reuse.

### _Reward Function:_

+ +200 for reaching the Cup
+ -150 for being caught by the Death Eater
+-1 per step (to encourage faster solutions)
+ -0.5 for revisiting cells
+ +proximity reward for moving closer to the Cup
+ +0.5 for moving away from the Death Eater

## How to Run:

### NOTE: No retraining is required to visualize the trained agent. One only needs to run ```TrainedModel.ipynb``` with ```q_table.pkl``` present. However, if one wishes to see how the model is being trained, and chart plots of __Reward per episode__ and the __Rolling Success Rate__, one can run the first code block in ```Code2.ipynb```

### Visualizing (```TrainedModel.ipynb```)
Open and run all cells in TrainedModel.ipynb.
The Pygame window will open, showing the trained agent navigating the maze.

### Training (```Code2.ipynb```)
__Install dependencies:__
```pip install numpy matplotlib pygame```
Run the first cell. The notebook will train the agent and save the Q-table to q_table.pkl at the end.
