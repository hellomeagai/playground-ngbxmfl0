

# Initialize pygame
pygame.init()

# Set display dimensions
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Pacman")

# Set colors
black = (0, 0, 0)
yellow = (255, 255, 0)

# Set Pacman attributes
pacman_radius = 20
pacman_x = screen_width // 2
pacman_y = screen_height // 2
pacman_direction = 0
pacman_speed = 5

# Set ghost attributes
ghost_radius = 20
ghost_x = random.randint(0, screen_width - ghost_radius * 2)
ghost_y = random.randint(0, screen_height - ghost_radius * 2)
ghost_direction = random.randint(0, 3)
ghost_speed = 3

# Set game loop
running = True
while running:
    screen.fill(black)
    
    # Quit game if 'X' button is clicked
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    # Move Pacman
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        pacman_direction = 180
        pacman_x -= pacman_speed
    if keys[pygame.K_RIGHT]:
        pacman_direction = 0
        pacman_x += pacman_speed
    if keys[pygame.K_UP]:
        pacman_direction = 90
        pacman_y -= pacman_speed
    if keys[pygame.K_DOWN]:
        pacman_direction = 270
        pacman_y += pacman_speed
    
    # Move Ghost
    if ghost_direction == 0:
        ghost_x += ghost_speed
    elif ghost_direction == 1:
        ghost_x -= ghost_speed
    elif ghost_direction == 2:
        ghost_y += ghost_speed
    else:
        ghost_y -= ghost_speed
    
    # Draw Pacman
    pygame.draw.circle(screen, yellow, (pacman_x, pacman_y), pacman_radius)
    
    # Draw Ghost
    pygame.draw.circle(screen, (255, 0, 0), (ghost_x, ghost_y), ghost_radius)
    
    # Update display
    pygame.display.update()

# Quit the game
pygame.quit()

