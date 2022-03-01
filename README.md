# html-ball-brick
classBall(GameObject):
def __init__(self, canvas, x, y):
self.radius = 10
self.direction = [1, -1]
self.speed = 10
item =canvas.create_oval(x-self.radius, y-self.radius,
x+self.radius, y+self.radius,
fill='white')
super(Ball, self).__init__(canvas,item)
  
def update(self):
coords = self.get_position()
width = self.canvas.winfo_width()
if coords[0] <= 0 or coords[2] >=width:
self.direction[0] *= -1
if coords[1] <= 0:
self.direction[1] *= -1
x = self.direction[0] * self.speed
y = self.direction[1] * self.speed
self.move(x, y)
  
def collide(self, game_objects):
coords = self.get_position()
x = (coords[0] + coords[2]) * 0.5
 if len(game_objects) > 1:
self.direction[1] *= -1
elif len(game_objects) == 1:
game_object = game_objects[0]
coords = game_object.get_position()
if x > coords[2]:
self.direction[0] = 1
elif x < coords[0]:
self.direction[0] = -1
else:
self.direction[1] *= -1
  
for game_object in game_objects:
if isinstance(game_object, Brick):
game_object.hit()
