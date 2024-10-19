import pygame
import random
import sys

pygame.init()

screen_size = 600
screen = pygame.display.set_mode((screen_size, screen_size))
pygame.display.set_caption("Minesweeper")

WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
GRAY = (192, 192, 192)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)

difficulty_levels = {
    "easy": (8, 10),
    "medium": (16, 40),
    "hard": (24, 99)
}

def choose_difficulty_screen():
    screen.fill(WHITE)
    easy_button = pygame.Rect(screen_size // 2 - 100, screen_size // 2 - 60, 200, 50)
    medium_button = pygame.Rect(screen_size // 2 - 100, screen_size // 2, 200, 50)
    hard_button = pygame.Rect(screen_size // 2 - 100, screen_size // 2 + 60, 200, 50)
    
    pygame.draw.rect(screen, GRAY, easy_button)
    pygame.draw.rect(screen, GRAY, medium_button)
    pygame.draw.rect(screen, GRAY, hard_button)
    
    easy_text = pygame.font.SysFont(None, 40).render("Easy", True, BLACK)
    medium_text = pygame.font.SysFont(None, 40).render("Medium", True, BLACK)
    hard_text = pygame.font.SysFont(None, 40).render("Hard", True, BLACK)
    
    screen.blit(easy_text, (easy_button.x + 50, easy_button.y + 10))
    screen.blit(medium_text, (medium_button.x + 30, medium_button.y + 10))
    screen.blit(hard_text, (hard_button.x + 50, hard_button.y + 10))
    
    pygame.display.flip()
    
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()
            elif event.type == pygame.MOUSEBUTTONDOWN:
                if easy_button.collidepoint(event.pos):
                    return "easy"
                elif medium_button.collidepoint(event.pos):
                    return "medium"
                elif hard_button.collidepoint(event.pos):
                    return "hard"

def create_grid(grid_size):
    grid = [[0 for _ in range(grid_size)] for _ in range(grid_size)]
    revealed = [[False for _ in range(grid_size)] for _ in range(grid_size)]
    flags = [[False for _ in range(grid_size)] for _ in range(grid_size)]
    return grid, revealed, flags

def location_mines(grid, num_mines):
    count = 0
    grid_size = len(grid)
    while count < num_mines:
        x = random.randint(0, grid_size - 1)
        y = random.randint(0, grid_size - 1)
        if grid[x][y] == 0:
            grid[x][y] = -1
            count += 1

def show_numbers(grid):
    grid_size = len(grid)
    for x in range(grid_size):
        for y in range(grid_size):
            if grid[x][y] == -1:
                continue
            count = 0
            for i in range(max(0, x-1), min(grid_size, x+2)):
                for j in range(max(0, y-1), min(grid_size, y+2)):
                    if grid[i][j] == -1:
                        count += 1
            grid[x][y] = count

def show_grid(screen, grid, revealed, flags):
    grid_size = len(grid)
    cell_size = screen_size // grid_size
    
    font_size = cell_size // 2
    font = pygame.font.SysFont(None, font_size)

    for x in range(grid_size):
        for y in range(grid_size):
            rect = pygame.Rect(x * cell_size, y * cell_size, cell_size, cell_size)
            if revealed[x][y]:
                if grid[x][y] == -1:
                    pygame.draw.rect(screen, RED, rect)
                else:
                    pygame.draw.rect(screen, GREEN, rect)
                    text = font.render(str(grid[x][y]), True, BLACK)
                    screen.blit(text, (x * cell_size + cell_size // 4, y * cell_size + cell_size // 4))
            else:
                pygame.draw.rect(screen, GRAY, rect)
                if flags[x][y]:
                    pygame.draw.circle(screen, BLUE, rect.center, cell_size // 4)
            pygame.draw.rect(screen, BLACK, rect, 1)

def check_win(grid, revealed):
    for x in range(len(grid)):
        for y in range(len(grid)):
            if grid[x][y] != -1 and not revealed[x][y]:
                return False
    return True

def show_end_screen(screen, message):
    screen.fill(WHITE)
    text = pygame.font.SysFont(None, 40).render(message, True, BLACK)
    screen.blit(text, (screen_size // 4 + 20, screen_size // 2))
    pygame.display.flip()
    pygame.time.wait(1000)

    button_rect = pygame.Rect(screen_size // 2 - 100, screen_size // 2 + 50, 200, 50)
    pygame.draw.rect(screen, GRAY, button_rect)
    button_text = pygame.font.SysFont(None, 40).render("Again", True, BLACK)
    screen.blit(button_text, (button_rect.x + 50, button_rect.y + 10))
    pygame.display.flip()

    waiting = True
    while waiting:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()
            elif event.type == pygame.MOUSEBUTTONDOWN:
                if button_rect.collidepoint(event.pos):
                    waiting = False

def main():
    difficulty = choose_difficulty_screen()
    grid_size, num_mines = difficulty_levels[difficulty]
    
    grid, revealed, flags = create_grid(grid_size)
    
    location_mines(grid, num_mines)
    
    show_numbers(grid)
    
    running = True
    game_over = False
    
    while running:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
            elif event.type == pygame.MOUSEBUTTONDOWN and not game_over:
                x, y = event.pos
                x //= screen_size // grid_size
                y //= screen_size // grid_size
                if event.button == 1:
                    revealed[x][y] = True
                    if grid[x][y] == -1:
                        game_over = True
                        show_end_screen(screen, "Game Over")
                        main()
                elif event.button == 3:
                    flags[x][y] = not flags[x][y]

        if check_win(grid, revealed):
            game_over = True
            show_end_screen(screen, "You Win!!!✧٩(ˊωˋ*)و✧")
            main()

        screen.fill(BLACK)
        show_grid(screen, grid, revealed, flags)
        pygame.display.flip()

    pygame.quit()

if __name__ == "__main__":
    main()
