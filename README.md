# 12444
import pygame

class Paddle(pygame.sprite.Sprite):
    def __init__(self, color, width, height):
        super().__init__()

        self.image = pygame.Surface([width, height])
        self.image.fill(color)

        self.rect = self.image.get_rect()

    def move_up(self, pixels):
        self.rect.y -= pixels
        if self.rect.y < 0:
            self.rect.y = 0

    def move_down(self, pixels):
        self.rect.y += pixels
        if self.rect.y > 400:
            self.rect.y = 400
import random

class Ball(pygame.sprite.Sprite):
    def __init__(self, color, width, height):
        super().__init__()

        self.image = pygame.Surface([width, height])
        self.image.fill(color)

        self.rect = self.image.get_rect()
        self.speed = 5
        self.direction = random.choice(["NE", "SE", "SW", "NW"])

    def update(self):
        if self.direction == "NE":
            self.rect.x += self.speed
            self.rect.y -= self.speed
        elif self.direction == "SE":
            self.rect.x += self.speed
            self.rect.y += self.speed
        elif self.direction == "SW":
            self.rect.x -= self.speed
            self.rect.y += self.speed
        elif self.direction == "NW":
            self.rect.x -= self.speed
            self.rect.y -= self.speed

        if self.rect.y < 0:
            if self.direction == "NE":
                self.direction = "SE"
            elif self.direction == "NW":
                self.direction = "SW"
        elif self.rect.y > 480:
            if self.direction == "SE":
                self.direction = "NE"
            elif self.direction == "SW":
                self.direction = "NW"

        if self.rect.x < 0:
            if self.direction == "SW":
                self.direction = "SE"
            elif self.direction == "NW":
                self.direction = "NE"
        elif self.rect.x > 620:
            if self.direction == "SE":
                self.direction = "SW"
            elif self.direction == "NE":
                self.direction = "NW"
all_sprites_list.update()

if ball.rect.x >= 700:
    score_left += 1
    ball.rect.x = 350
    ball.rect.y = 250
elif ball.rect.x <= 0:
    score_right += 1
    ball.rect.x = 350
    ball.rect.y = 250

# Check if the ball is hitting the paddle and change its direction accordingly
if pygame.sprite.collide_mask(ball, player_paddle) or pygame.sprite.collide_mask(ball, computer_paddle):
    ball.speed += 1
    ball.direction = random.choice(["NE", "SE", "SW", "NW"])
    beep_sound.play()
font = pygame.font.Font(None, 36)

text = font.render("Player: {}   Computer: {}".format(score_left, score_right), 1, (255, 255, 255))
screen.blit(text, (250, 10))

if score_left == 10:
    text = font.render("Player wins!", 1, (255, 255, 255))
    screen.blit(text, (250, 200))
    pygame.display.flip()
    pygame.time.wait(3000)
    done = True
elif score_right == 10:
    text = font.render("Computer wins!", 1, (255, 255, 255))
    screen.blit(text, (250, 200))
    pygame.display.flip()
    pygame.time.wait(3000)
    done = True
