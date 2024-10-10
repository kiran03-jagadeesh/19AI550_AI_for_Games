### Ex.No: 10 Implementation of Negamax algorithm 
### DATE:10.10.2024
### REGISTER NUMBER :212221240022
# AIM:
Write a negamax algorithm to find the optimal value of Player from the graph.

# Steps:
1.Start the program
2.Define the minimax function
3.If maximum depth is reached then return the score value of leaf node. [depth taken as 3]
4.In Max player turn, assign the  maximum value by calling the negamax function recursively.
5.In Min player turn, finding the maximum value by taking the negation of its children.
6.Specify the score value of leaf nodes and Call the negamax function.
7.Print the best value of Max player.
8.Stop the program.
## Program:
```
import random

# Initialize game grid
grid = [[None for _ in range(10)] for _ in range(10)]

# Set player starting position
player_x, player_y = 0, 0

# Set treasure chamber position
treasure_x, treasure_y = 9, 9

# Initialize player HP
player_hp = 10

# Function to generate random treasure and monster locations
def generate_game():
    for i in range(10):
        for j in range(10):
            if random.random() < 0.1:
                grid[i][j] = "treasure"
            elif random.random() < 0.05:
                grid[i][j] = "monster"

# Function to handle player movement
def move_player(dx, dy):
    global player_x, player_y
    new_x, new_y = player_x + dx, player_y + dy
    if 0 <= new_x < 10 and 0 <= new_y < 10:
        player_x, player_y = new_x, new_y

# Function to handle battles
def battle_monster():
    global player_hp
    player_hp -= 1

# Negamax algorithm
def negamax(node, depth, alpha, beta, is_maximizing_player):
    if depth == 0 or node.is_terminal():
        return node.evaluate()

    if is_maximizing_player:
        value = -float('inf')
        for child in node.children:
            value = max(value, -negamax(child, depth - 1, -beta, -alpha, False))
            alpha = max(alpha, value)
            if alpha >= beta:
                break
        return value
    else:
        value = float('inf')
        for child in node.children:
            value = min(value, -negamax(child, depth - 1, -beta, -alpha, True))
            beta = min(beta, value)
            if beta <= alpha:
                break
        return value

# Node class
class Node:
    def __init__(self, x, y, hp, treasure, monster):
        self.x = x
        self.y = y
        self.hp = hp
        self.treasure = treasure
        self.monster = monster
        self.children = []

    def is_terminal(self):
        return self.hp <= 0 or self.x == treasure_x and self.y == treasure_y

    def evaluate(self):
        if self.hp <= 0:
            return -100  # lose
        elif self.x == treasure_x and self.y == treasure_y:
            return 100  # win
        else:
            return self.treasure  # intermediate state

    def generate_children(self):
        # generate children nodes based on possible moves
        for dx, dy in [(0, -1), (0, 1), (-1, 0), (1, 0)]:
            new_x, new_y = self.x + dx, self.y + dy
            if 0 <= new_x < 10 and 0 <= new_y < 10:
                new_hp = self.hp
                new_treasure = self.treasure
                new_monster = self.monster
                if grid[new_x][new_y] == "treasure":
                    new_treasure += 1
                elif grid[new_x][new_y] == "monster":
                    new_hp -= 1
                child = Node(new_x, new_y, new_hp, new_treasure, new_monster)
                self.children.append(child)

# Main game loop
generate_game()

while True:
    # Display game grid
    print("Game Grid:")
    for row in grid:
        print(" ".join(str(cell) if cell else "." for cell in row))

    # Get player input
    move = input("Enter a direction (up, down, left, right): ")

    # Handle player movement
    if move == "up":
        move_player(0, -1)
    elif move == "down":
        move_player(0, 1)
    elif move == "left":
        move_player(-1, 0)
    elif move == "right":
        move_player(1, 0)

        # Check for treasure or monsters
    if grid[player_x][player_y] == "treasure":
        print("You found treasure!")
    elif grid[player_x][player_y] == "monster":
        battle_monster()
        print("You fought a monster!")

    # Use Negamax algorithm to find optimal value
    root = Node(player_x, player_y, player_hp, 0, False)
    root.generate_children()
    best_value = negamax(root, 5, -float('inf'), float('inf'), True)
    print("Optimal value:", best_value)

    # Update game state
    if player_hp <= 0:
        print("You lost! Game over.")
        break
    elif player_x == treasure_x and player_y == treasure_y:
        print("You won! Congratulations!")
        break
```


## Output:
![image](https://github.com/user-attachments/assets/3e8c6f53-7e66-4469-86ab-3ec1b869e92b)

## RESULT
Thus the best score of max player was found using negamax algorithm
