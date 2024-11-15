# Ex.No: 11 Mini Project  
### DATE:  
### REGISTER NUMBER: 212221240022

### AIM:  
To write a Python program to simulate a game using **Pygame**.

### Algorithm:
1. **Initialize Pygame:**
   - Import the `pygame` library and initialize it.
   
2. **Set up the game window:**
   - Define the width and height of the game window.
   - Use `pygame.display.set_mode()` to create the window.
   - Set a title for the game window.

3. **Load game elements:**
   - Load images for the player and enemy using `pygame.image.load()`.
   - Set initial positions for the player and enemy.

4. **Handle user input:**
   - In the game loop, check for user inputs (left, right, and quit).
   - Update the player's position based on the input.
   
5. **Implement game logic:**
   - Set boundaries for the player's movement so they don’t move outside the game window.

6. **Draw elements on the screen:**
   - Clear the screen in each iteration.
   - Draw the player and enemy images at their respective positions.
   
7. **Add sound effects:**
   - Initialize `pygame.mixer` and load a sound.
   - Play the sound when a specific key (e.g., spacebar) is pressed.

8. **Game loop:**
   - Continue running the game until the user quits.
   - Use `pygame.event.get()` to handle events and `pygame.display.flip()` to update the screen.

9. **Quit the game:**
   - Use `pygame.quit()` to close the game when the loop ends.

### Program:
```python
import pygame

# Initialize Pygame
pygame.init()

# Set up the display
width, height = 800, 600
screen = pygame.display.set_mode((width, height))
pygame.display.set_caption("My Pygame")

# Load player and enemy images
player_image = pygame.image.load("player.png")
enemy_image = pygame.image.load("enemy.png")
player_x, player_y = 400, 500
enemy_x, enemy_y = 300, 100

# Initialize sound
pygame.mixer.init()
sound_effect = pygame.mixer.Sound("sound.wav")

# Game loop
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                running = False
            if event.key == pygame.K_SPACE:
                sound_effect.play()

    # Update player position
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x > 0:
        player_x -= 5
    if keys[pygame.K_RIGHT] and player_x < width - player_image.get_width():
        player_x += 5

    # Clear the screen
    screen.fill((0, 0, 0))

    # Draw player and enemy
    screen.blit(player_image, (player_x, player_y))
    screen.blit(enemy_image, (enemy_x, enemy_y))

    # Update display
    pygame.display.flip()

# Quit the game
pygame.quit()

### Output:
A game window is created with a player character that can move left and right using the arrow keys. Pressing the spacebar plays a sound. The game continues running until the user quits by closing the window or pressing the escape key.

### Result:
Thus, the simple game was implemented using Pygame.
