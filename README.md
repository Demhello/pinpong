from pygame import *
from random import *

game = True
lose1 = False
lose2 = False
dx = 5
dy = 3
font.init()
font1 = font.Font(None, 50)


scr = display.set_mode((800,600))
back = transform.scale(image.load("galaxy.jpg"),(800,600))

class obekt(sprite.Sprite):
    def __init__(self, picimage, sx,sy,sspeed):
        super().__init__()
        self.image = transform.scale(image.load(picimage),(30,120))
        self.speed = sspeed
        self.rect = self.image.get_rect()
        self.rect.x = sx
        self.rect.y = sy
    def reset(self):
        scr.blit(self.image,(self.rect.x,self.rect.y))

class obekt2(sprite.Sprite):
    def __init__(self, picimage, sx,sy,sspeed):
        super().__init__()
        self.image = transform.scale(image.load(picimage),(50,50))
        self.speed = sspeed
        self.rect = self.image.get_rect()
        self.rect.x = sx
        self.rect.y = sy
    def reset(self):
        scr.blit(self.image,(self.rect.x,self.rect.y))

class igrok(obekt):
    def update(self):
        keys_pressed = key.get_pressed()
        if keys_pressed[K_s] and self.rect.y < 480:
            self.rect.y += 5
        if keys_pressed[K_w] and self.rect.y > 0:
            self.rect.y -= 5

class igrok2(obekt):
    def update(self):
        keys_pressed = key.get_pressed()
        if keys_pressed[K_DOWN] and self.rect.y < 480:
            self.rect.y += 5
        if keys_pressed[K_UP] and self.rect.y > 0:
            self.rect.y -= 5

class balls(obekt2):
    def update(self):
        global dx,dy,game,lose1,lose2
        self.rect.x += dx
        self.rect.y -= dy
        if sprite.collide_rect(self,ping2):
            dx *= -1
        if sprite.collide_rect(self,ping1):
            dx *= -1
        if self.rect.y > 570:
            dy *= -1
        if self.rect.y < 0:
            dy *= -1
        if self.rect.x > 800:
            lose2 = True
            game = False
        if self.rect.x < 0:
            lose1 = True
            game = False

ping1 = igrok("ping.png", 6,200, 4)
ping2 = igrok2("ping.png", 765,200, 4)
ball = balls("maz.png", 300,250,5)

while game:
    scr.blit(back,(0,0))
    for e in event.get():
        if e.type == QUIT:
            game = False
    ping1.reset()
    ping1.update()
    ping2.reset()
    ping2.update()
    ball.reset()
    ball.update()
    display.update()
while lose1:
    lose1txt = "Победил игрок 2"
    lose1text = font1.render(lose1txt, 1, (255,0,0))
    scr.blit(back,(0,0))
    scr.blit(lose1text, (200,200))
    for e in event.get():
        if e.type == QUIT:
            lose1 = False
    display.update()
while lose2:
    lose2txt = "Победил игрок 1"
    lose2text = font1.render(lose2txt, 1, (255,0,0))
    scr.blit(back,(0,0))
    scr.blit(lose2text, (200,200))
    for e in event.get():
        if e.type == QUIT:
            lose2 = False
    display.update()
