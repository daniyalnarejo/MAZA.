import streamlit as st
import numpy as np
import pygame
from pygame.locals import *
from random import randint

# Initialize Streamlit app
st.title("Maze Solver Game on Streamlit")
st.markdown("Navigate through the maze to reach the goal! Use the arrow keys to move.")

# Initialize Pygame
def initialize_game():
    pygame.init()
    screen = pygame.display.set_mode((600, 600))
    pygame.display.set_caption('Maze Solver')
    return screen

# Define game constants
GRID_SIZE = 20
CELL_SIZE = 30
PLAYER_COLOR = (0, 255, 0)
GOAL_COLOR = (255, 0, 0)
WALL_COLOR = (0, 0, 255)
BG_COLOR = (0, 0, 0)
FPS = 60

# Generate a random maze
def generate_maze(rows, cols):
    maze = [[1 if randint(0, 4) > 0 else 0 for _ in range(cols)] for _ in range(rows)]
    maze[0][0] = 0  # Start point
    maze[rows-1][cols-1] = 0  # Goal point
    return maze

# Draw the maze
def draw_maze(screen, maze):
    for row in range(len(maze)):
        for col in range(len(maze[0])):
            color = WALL_COLOR if maze[row][col] == 1 else BG_COLOR
            pygame.draw.rect(screen, color, pygame.Rect(col * CELL_SIZE, row * CELL_SIZE, CELL_SIZE, CELL_SIZE))

# Draw the player
def draw_player(screen, player_pos):
    pygame.draw.rect(screen, PLAYER_COLOR, pygame.Rect(player_pos[1] * CELL_SIZE + 5, player_pos[0] * CELL_SIZE + 5, CELL_SIZE - 10, CELL_SIZE - 10))

# Draw the goal
def draw_goal(screen, goal_pos):
    pygame.draw.rect(screen, GOAL_COLOR, pygame.Rect(goal_pos[1] * CELL_SIZE + 5, goal_pos[0] * CELL_SIZE + 5, CELL_SIZE - 10, CELL_SIZE - 10))

# Main game function
def maze_solver():
    screen = initialize_game()
    clock = pygame.time.Clock()

    rows, cols = 20, 20
    maze = generate_maze(rows, cols)
    player_pos = [0, 0]  # Starting position
    goal_pos = [rows - 1, cols - 1]  # Goal position

    running = True
    while running:
        screen.fill(BG_COLOR)
        draw_maze(screen, maze)
        draw_player(screen, player_pos)
        draw_goal(screen, goal_pos)

        for event in pygame.event.get():
            if event.type == QUIT:
                running = False

        keys = pygame.key.get_pressed()
        if keys[K_UP] and player_pos[0] > 0 and maze[player_pos[0] - 1][player_pos[1]] == 0:
            player_pos[0] -= 1
        if keys[K_DOWN] and player_pos[0] < rows - 1 and maze[player_pos[0] + 1][player_pos[1]] == 0:
            player_pos[0] += 1
        if keys[K_LEFT] and player_pos[1] > 0 and maze[player_pos[0]][player_pos[1] - 1] == 0:
            player_pos[1] -= 1
        if keys[K_RIGHT] and player_pos[1] < cols - 1 and maze[player_pos[0]][player_pos[1] + 1] == 0:
            player_pos[1] += 1

        if player_pos == goal_pos:
            st.success('Congratulations! You reached the goal!')
            running = False

        pygame.display.flip()
        clock.tick(FPS)

# Deploying in Streamlit
if st.button('Start Game'):
    maze_solver()
