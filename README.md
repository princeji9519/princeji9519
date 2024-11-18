import pygame
import math

# Initialize Pygame
pygame.init()

# Set up the display
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Solar System Simulation")

# Define colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
YELLOW = (255, 255, 0)
BLUE = (30, 144, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
MARS_RED = (255, 69, 0)

# Define the central sun
sun_radius = 50
sun_pos = (screen_width // 2, screen_height // 2)

# Planetary parameters (radius, color, orbital radius, orbital speed)
planets = [
    {'name': 'Mercury', 'color': (169, 169, 169), 'orbital_radius': 70, 'speed': 0.047},
    {'name': 'Venus', 'color': (255, 223, 0), 'orbital_radius': 100, 'speed': 0.035},
    {'name': 'Earth', 'color': BLUE, 'orbital_radius': 150, 'speed': 0.02},
    {'name': 'Mars', 'color': MARS_RED, 'orbital_radius': 200, 'speed': 0.015},
    {'name': 'Jupiter', 'color': (255, 165, 0), 'orbital_radius': 300, 'speed': 0.008},
    {'name': 'Saturn', 'color': (255, 255, 0), 'orbital_radius': 400, 'speed': 0.005},
]

# Set up the clock for controlling the frame rate
clock = pygame.time.Clock()

# Initialize the angle for orbital movement
planet_angles = {planet['name']: 0 for planet in planets}

# Main game loop
running = True
while running:
    # Handle events (for closing the window)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Fill the background with black
    screen.fill(BLACK)

    # Draw the Sun
    pygame.draw.circle(screen, YELLOW, sun_pos, sun_radius)

    # Update and draw planets
    for planet in planets:
        # Get the orbital radius and speed
        orbital_radius = planet['orbital_radius']
        speed = planet['speed']

        # Update the angle for the planet's orbit
        planet_angles[planet['name']] += speed

        # Calculate the planet's position
        x = sun_pos[0] + orbital_radius * math.cos(planet_angles[planet['name']])
        y = sun_pos[1] + orbital_radius * math.sin(planet_angles[planet['name']])

        # Draw the planet
        pygame.draw.circle(screen, planet['color'], (int(x), int(y)), 15)

    # Update the display
    pygame.display.flip()

    # Limit the frame rate to 60 FPS
    clock.tick(60)

# Quit Pygame
pygame.quit()
