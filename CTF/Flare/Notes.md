## Level 1
The code has a block class with the passable parameter, if we force it to be True, we can "clip through walls".
```
class Block(pygame.sprite.Sprite):
    def __init__(self, x, y, passable):
        super().__init__()
        self.image = blockimage
        self.rect = self.image.get_rect()
        self.x = x
        self.y = y
        self.passable = True # Here i modified the variable
        self.rect.top = self.y * tile_size
        self.rect.left = self.x * tile_size

    def draw(self, surface):
        surface.blit(self.image, self.rect)
```
Then open the game and easy as that, we can clip through the wall.
## Level 2
Decompiled golang code... what the hell.
Two things:
There's some chacha20 involved and main is splitted in main.a and main.b
main.b in the end calls os.Exit(0xdeadbeef) so it might be a fake road? 
So far: if the first parameter of main.b is 0 then the program exits with code 0xdeadbeef, else it allocates new stack?