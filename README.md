# Asteroid Game Technical Documentation

A classic arcade-style asteroid shooting game implemented in Python using the Pygame library.

## Project Overview

This project is a 2D space shooter game where the player controls a triangular spaceship that can rotate and move around the screen. The objective is to destroy asteroids by shooting them while avoiding collisions. When hit, larger asteroids split into smaller ones, increasing the challenge as the game progresses.

## Technical Architecture

### Core Components

1. **Game Engine**: Built on Pygame for rendering, input handling, and game loop management
2. **Object-Oriented Design**: Uses inheritance for game objects with a base `CircleShape` class
3. **Collision Detection**: Simple circle-based collision system
4. **Sprite Management**: Utilizes Pygame's sprite groups for efficient updates and rendering

### Module Structure

- **main.py**: Entry point and game loop controller
- **constants.py**: Game configuration parameters
- **circleshape.py**: Base class for all game objects
- **player.py**: Player spaceship implementation
- **asteroid.py**: Asteroid object implementation
- **asteroidfield.py**: Asteroid spawning and management
- **shot.py**: Player projectile implementation

## Class Hierarchy

```
CircleShape (Base Class)
├── Player
├── Asteroid
└── Shot
```

## Detailed Module Documentation

### main.py

The main game controller that initializes the game, manages the game loop, and handles collision detection.

**Key Functions:**
- `main()`: Initializes Pygame, sets up sprite groups, and runs the game loop

**Game Loop Operations:**
1. Process user input events
2. Update all game objects
3. Check for collisions between objects
4. Render all drawable objects
5. Maintain frame rate at 60 FPS

### circleshape.py

Base class for all game objects that provides common functionality.

**Key Properties:**
- `position`: 2D vector representing object position
- `velocity`: 2D vector representing object movement
- `radius`: Object collision radius

**Key Methods:**
- `collides_with(other)`: Detects collision with another CircleShape object
- `draw(screen)`: Abstract method for rendering the object
- `update(dt)`: Abstract method for updating object state

### player.py

Implements the player-controlled spaceship.

**Key Properties:**
- `rotation`: Current angle of the spaceship
- `shoot_timer`: Cooldown timer for shooting

**Key Methods:**
- `triangle()`: Calculates the three points of the player's triangular shape
- `rotate(dt)`: Rotates the player based on input
- `move(dt)`: Moves the player in the direction it's facing
- `shoot()`: Creates a new Shot object if cooldown allows

### asteroid.py

Implements the asteroid objects that the player must avoid and destroy.

**Key Methods:**
- `split()`: Breaks the asteroid into two smaller asteroids when hit
- `update(dt)`: Updates asteroid position based on velocity

### asteroidfield.py

Manages the spawning of asteroids from the edges of the screen.

**Key Properties:**
- `edges`: Defines the four edges of the screen for asteroid spawning
- `spawn_timer`: Controls the rate of asteroid spawning

**Key Methods:**
- `spawn(radius, position, velocity)`: Creates a new asteroid with specified parameters
- `update(dt)`: Manages the spawn timer and creates new asteroids

### shot.py

Implements the projectiles fired by the player.

**Key Methods:**
- `update(dt)`: Updates shot position based on velocity

### constants.py

Defines game configuration parameters:

- Screen dimensions: `SCREEN_WIDTH`, `SCREEN_HEIGHT`
- Asteroid properties: `ASTEROID_MIN_RADIUS`, `ASTEROID_KINDS`, `ASTEROID_SPAWN_RATE`
- Player properties: `PLAYER_RADIUS`, `PLAYER_TURN_SPEED`, `PLAYER_SPEED`, `PLAYER_SHOOT_SPEED`, `PLAYER_SHOOT_COOLDOWN`
- Shot properties: `SHOT_RADIUS`

## Game Mechanics

### Movement System

The player ship uses a simple physics model:
- Forward/backward movement in the direction the ship is facing
- Rotation controlled independently of movement
- Constant velocity (no acceleration/deceleration)

### Collision System

Collision detection uses circle-based hitboxes:
- Objects collide when the distance between their centers is less than the sum of their radii
- Player collision with asteroids ends the game
- Shot collision with asteroids splits the asteroid and removes the shot

### Asteroid Spawning

Asteroids spawn from the edges of the screen with:
- Random edge selection
- Random speed between 40-100 units
- Random direction variation (±30 degrees from perpendicular to edge)
- Random size (1-3 times the minimum radius)

### Asteroid Splitting

When hit by a shot:
- Asteroids split into two smaller asteroids
- New asteroids travel at angles 20-50 degrees from the original
- New asteroids move 20% faster than the original
- Asteroids that reach minimum size are destroyed without splitting

## Setup and Usage

### Requirements

- Python 3.x
- Pygame library

### Installation

1. Ensure Python is installed on your system
2. Install Pygame: `pip install pygame`
3. Clone or download this repository

### Running the Game

Execute the main script:
```
python main.py
```

### Controls

- **W**: Move forward
- **S**: Move backward
- **A**: Rotate counter-clockwise
- **D**: Rotate clockwise
- **Spacebar**: Shoot
