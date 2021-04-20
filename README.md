# pinpong
from pygame import *
from random import *

game = True

scr = display.set_mode((1000,600))
back = transform.scale(image.load("galaxy.jpg"),(1000,600))

class obekt(sprite.Sprite):
    def __init__(self, picimage, sx,sy,sspeed):
        super().__init__()
        self.image = transform.scale(image.load(picimage),(500,300))
        self.speed = sspeed
        self.rect = self.image.get_rect()
        self.rect.x = sx
        self.rect.y = sy
    def reset(self):
        scr.blit(self.image,(self.rect.x,self.rect.y))

class igrok(obekt):
    def update(self):
        global b,patron,n,game,shop
        keys_pressed = key.get_pressed()
        if keys_pressed[K_s] and self.rect.x < 900:
            self.rect.y += 5
        if keys_pressed[K_w] and self.rect.x > 5:
            self.rect.y -= 5

class igrok2(obekt):
    def update(self):
        global b,patron,n,game,shop
        keys_pressed = key.get_pressed()
        if keys_pressed[K_DOWN] and self.rect.x < 900:
            self.rect.y += 5
        if keys_pressed[K_UP] and self.rect.x > 5:
            self.rect.y -= 5

ping1 = igrok("ping.png", 450,520, 6)
ping2 = igrok2("ping.png", 450,520, 6)

while game:
    scr.blit(back,(0,0))
    for e in event.get():
        if e.type == QUIT:
            game = False
    ping1.reset()
    ping1.update()
    ping2.reset()
    ping2.update()
    display.update()
