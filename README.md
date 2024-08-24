# Flappy Bird AI with NEAT

This project implements a Flappy Bird-like game where the bird's behavior is controlled by a neural network optimized using the NEAT (NeuroEvolution of Augmenting Topologies) algorithm. The goal is to evolve neural networks to maximize the bird's survival time and score in the game.

## Project Overview:
- **Game Engine:** Pygame (game development framework)
- **AI Algorithm:** NEAT (NeuroEvolution of Augmenting Topologies)
- **Game Objective:** Evolve a neural network to guide the bird through an endless series of pipes

## Files:
- **main.py:** The main script that runs the game and NEAT algorithm
- **imgs/:** Directory containing images used in the game (bird sprites, pipes, background, base)
- **neat.txt:** NEAT configuration file
- **best_genome.pkl:** File where the best genome is saved after training

## Game Description:
- The bird's goal is to navigate through pipes by jumping at appropriate times
- The game's logic and AI training are handled by NEAT, which evolves a population of neural networks to improve their performance over generations

## Key Components:

### Classes:
- **Bird:**
  - **Attributes:**
    - `x, y`: Position of the bird
    - `tilt`: Rotation angle for animation
    - `tick_count, vel, height, img_count, img`: Various properties for movement and animation
  - **Methods:**
    - `jump()`: Makes the bird jump
    - `move()`: Updates the bird's position and rotation based on physics
    - `draw(win)`: Draws the bird on the screen with appropriate animation
    - `get_mask()`: Returns a mask for collision detection

- **Pipe:**
  - **Attributes:**
    - `x, height, gap, top, bottom`: Position and size of the pipe
  - **Methods:**
    - `set_height()`: Randomly sets the height of the pipe
    - `move()`: Moves the pipe horizontally
    - `draw(win)`: Draws the pipe on the screen
    - `collide(bird)`: Checks if the pipe collides with the bird

- **Base:**
  - **Attributes:**
    - `y, x1, x2`: Position of the base
  - **Methods:**
    - `move()`: Moves the base to create a scrolling effect
    - `draw(win)`: Draws the base on the screen

### Functions:
- **`draw_window(win, birds, pipes, base, score, gen)`**
  - Draws all game components (birds, pipes, base) on the screen along with the score and generation number

- **`main(genomes, config)`**
  - Initializes the NEAT algorithm and game environment
  - Runs the game loop where neural networks control the birds
  - Updates fitness scores and handles game events

- **`run(config_path)`**
  - Configures and runs the NEAT algorithm to evolve neural networks
  - Saves the best genome found during the evolution

- **`run_with_winner(winner, config)`**
  - Runs a simulation with the best genome found, allowing visualization of the evolved neural network's performance

## Pickle Module Usage:
- **Saving the Best Genome:**
  - After the NEAT algorithm completes training, the best genome is saved to a file named `best_genome.pkl` using the pickle module. This allows you to persist the best-performing neural network across different runs

## Setup and Usage:
- **Install Dependencies:**
  - Ensure you have Python 3 installed
  - Install required libraries by typing: `pip install pygame neat-python` in the console

- **Run the Game and Training:**
  - Ensure the `imgs` directory contains the necessary image files
  - Run the main script by typing `python main.py` in the console

- **NEAT Configuration:**
  - Modify `neat.txt` to adjust NEAT parameters like population size, mutation rates, etc.

## NEAT Configuration:
- The NEAT configuration file `neat.txt` contains parameters for:
  - Population size
  - Number of generations
  - Mutation rates
  - Crossover rates
  - Fitness evaluation

## Visualize the Best Genome:
- After training, the best genome can be visualized by running the simulation with the best genome. Type in the console:
  ```python
  with open("best_genome.pkl", "rb") as f:
      winner = pickle.load(f)
  run_with_winner(winner, config)
  ```

## Notes:
- Ensure that the image files are correctly placed in the `imgs` directory to avoid missing assets
- The game will run for up to 50 generations or until a bird reaches a score of 50
