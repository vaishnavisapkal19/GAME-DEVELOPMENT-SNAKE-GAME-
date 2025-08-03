# GAME-DEVELOPMENT-SNAKE-GAME-

COMPANY NAME:- CODTECH IT SOLUTIONS

NAME:- SAPKAL VAISHNAVI GANESH 

INTERN ID:-CTO8DG447 

DOMAIN:- C++

DURATION:- 8 WEEKS

MENTOR:- NEELA SANTOSH

DISCRIPTION:- 1) Game setup: grid, window, and resources
The program opens by defining a fixed grid: the screen is WIDTH=800×HEIGHT=600 pixels, cells are 20×20, giving ROWS=30 and COLS=40. This grid‐based layout is standard for Snake games built with SFML, as illustrated in many C++ SFML Snake tutorials 
Packt
GitHub
.
Inside the SnakeGame struct, the constructor:

Creates an SFML RenderWindow sized to 800×600, sets a 60 FPS cap via setFramerateLimit(60).

Seeds random once with srand(time(nullptr)).

Places the snake’s initial head at the centre of the grid: (COLS/2, ROWS/2).

Calls spawnFood() to place one red food block in a random empty cell.

Loads sound files (eat.wav, game_over.wav) into sf::SoundBuffer and associates them with sf::Sound objects (eatSound, gameOverSound).

2) Data structures & coordinate mapping
The snake is stored as a std::deque<sf::Vector2i>, where each element represents a grid‐cell (x,y). The front of the deque is the head, and the back is the tail.
The food is a single sf::Vector2i.
Movement directions are enumerated with enum Direction { UP, DOWN, LEFT, RIGHT }. The initial direction is RIGHT.

3) Food placement (spawnFood)
This method loops until it finds a random (x,y) that doesn’t overlap the snake’s body, using std::find. That ensures you never spawn food inside the snake, a best practice seen in other SFML Snake implementations 
CodePal
+1
Stack Overflow
+1
.

4) Input handling (processInput)
Inside the main loop, the code processes SFML events:

If the window is closed, it calls window.close().

If arrow keys are pressed, it updates the direction, preventing reversal. For example, pressing Up while snake is moving Down does nothing, which avoids self‑collisions.

5) Game logic update (update())
Called only when enough time elapsed since last move (clock.getElapsedTime().asSeconds() >= speed). Default speed = 0.15f sec per grid step.

First, move the head one cell in the current direction.

Then check for collisions: if new head position is outside the grid or matches any body segment via std::find, set isGameOver = true and play gameOverSound, then return.

Otherwise, push the new head to the front of the deque. If the snake ate the food (head == food), it plays eatSound, calls spawnFood(), and increases difficulty by decreasing speed to a minimum of about 0.05 seconds per move. If no food was eaten, it pops the back tail segment so the length stays the same.

6) Rendering (render())
Every frame, the window is cleared to black, then the code draws grid‑aligned blocks of size (BLOCK_SIZE − 1) for slight separation.

The snake’s segments are drawn in green by iterating through the deque.

The food is drawn in red.

If isGameOver is true, it loads the DejaVu Sans Bold font (hardcoded), creates a sf::Text saying “Game Over!” in white at the center, and draws it. Finally window.display() shows the frame.

7) Main loop
run() loops while the window stays open. Each frame it:

Processes input events.

If not game over, calls update().

Always calls render().

8) Overall structure and gameplay
This minimal‑state single‑file C++ game cleanly combines SFML’s window/event system, deque for the snake body, time‑based movement using sf::Clock, and incremental difficulty by speeding up moves over time.
You grow longer with each food eaten, and the game ends when you hit a wall or yourself. That mirrors many classic Snake games and C++ SFML examples 
CodePal
+1
CodePal
+1
Reddit
.

9) Possible extensions
One could add:

Scoring system or high score display.

Smoother movement (interpolated or frame‑rate independent).

A menu, restart on keypress, or teleport wrap‑around behavior.

Improved font handling (font loaded once rather than every frame).

Better modular code: separate Snake, Food, and Game classes.
.




