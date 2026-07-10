How to draw a circle?
https://www.geeksforgeeks.org/python/how-to-draw-a-circle-using-matplotlib-in-python/

Demonstrating use of matplotlib.patches.Circle() function to plot a colored Circle

```

import matplotlib.pyplot as plt

figure, axes = plt.subplots()
Drawing_colored_circle = plt.Circle(( 0.6 , 0.6 ), 0.2 )

axes.set_aspect( 1 )
axes.add_artist( Drawing_colored_circle )
plt.title( 'Colored Circle' )
plt.show()
```


https://nickcharlton.net/posts/drawing-animating-shapes-matplotlib.html


```
import numpy as np
from matplotlib import pyplot as plt
from matplotlib import animation

fig = plt.figure()
fig.set_dpi(100)
fig.set_size_inches(7, 6.5)

ax = plt.axes(xlim=(0, 10), ylim=(0, 10))
patch = plt.Circle((5, -5), 0.75, fc='y')

def init():
    patch.center = (5, 5)
    ax.add_patch(patch)
    return patch,

def animate(i):
    x, y = patch.center
    x = 5 + 3 * np.sin(np.radians(i))
    y = 5 + 3 * np.cos(np.radians(i))
    patch.center = (x, y)
    return patch,

anim = animation.FuncAnimation(fig, animate, 
                               init_func=init, 
                               frames=360, 
                               interval=20,
                               blit=True)

plt.show()
```

https://en.wikipedia.org/wiki/Newton%27s_law_of_universal_gravitation


```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle

  

fig = plt.figure()

axis = plt.axes(xlim =(0, 4),

ylim =(-2, 2))

  

fig = plt.figure()

fig.set_dpi(100)

fig.set_size_inches(7, 6.5)

  

ax = plt.axes(xlim=(0, 10), ylim=(0, 10))

earth = Circle((5, -5), 0.75, fc='blue')

moon = Circle((5, -5), 0.2, fc='grey')

  

earth_mass = 10.0

moon_mass = 3.0

  

earth_pos = np.array([5.0, 5.0])

moon_pos = np.array([5.0, 8.0])

  

moon_vel = np.array([0.03, 0.0])

  

GRAV_CONSTANT = 0.0001

  

dt = 0.1

  

def init():

ax.add_patch(earth)

ax.add_patch(moon)

  

return earth, moon,

  
  

def calculate_gravity(mass1, mass2):

displacement = earth_pos - moon_pos

unit = displacement/np.linalg.norm(displacement)

print(displacement)

gravitational_force = GRAV_CONSTANT * ((mass1 * mass2)/np.square(np.linalg.norm(displacement)))*unit

return gravitational_force

  
  

def animate(i):

global moon_pos

global moon_vel

  

moon_vel += calculate_gravity(moon_mass, earth_mass)

moon_pos += moon_vel

earth.center = earth_pos

moon.center = moon_pos

  

return earth, moon,

  

anim = FuncAnimation(fig, animate,

init_func=init,

frames=360,

interval=20,

blit=True)

  

plt.show()
```


### 1. The Core Data You Need

Every frame, your game engine already knows two things about your spaceship:

- `r` (Position vector): The 2D distance vector from the center of the planet to your ship $(x, y)$.
    
- `v` (Velocity vector): How fast and in what 2D direction your ship is moving $(\Delta x, \Delta y)$.
    

You also need to know `μ` (Mu), which is just the gravitational constant times the mass of your planet ($G \times M$). This defines how strong the planet's gravity is.

### 2. The Math to Find the Shape

To draw the ellipse, your code needs to find the size of the orbit and which way it is rotated.

**Step A: Find the Size (Semi-major axis, $a$)**

You use the vis-viva equation to find the total energy of the orbit, which tells you how big the orbit is:

$$\frac{1}{a} = \frac{2}{|r|} - \frac{|v|^2}{\mu}$$

**Step B: Find the Shape and Rotation (Eccentricity Vector, $\vec{e}$)**

This is the secret weapon of 2D orbital math. The eccentricity vector points directly toward the **periapsis** (the lowest point of the orbit), and its length tells you how stretched out the orbit is.

$$\vec{e} = \frac{(|v|^2 - \frac{\mu}{|r|})\vec{r} - (\vec{r} \cdot \vec{v})\vec{v}}{\mu}$$

From $\vec{e}$, you get two critical numbers:

1. **Orbit Stretch (`e_length`):** The magnitude of $\vec{e}$. If it's $0$, it's a perfect circle. If it's between $0$ and $1$, it's an ellipse. If it's $\ge 1$, it's an escape trajectory (hyperbola).
    
2. **Orbit Rotation (`orbit_angle`):** The angle of $\vec{e}$ using `atan2(e.y, e.x)`. This tells you how many degrees the orbit is rotated around the planet.
    

### 3. Writing the Loop to Plot the Points

Now that your code knows the size ($a$), the stretch ($e$), and the rotation, you can use a `for` loop to calculate the points of the line.

Instead of time, you loop through **angles** (from $0$ to $360^\circ$). The polar equation for an orbit gives you the distance ($radius$) at any given angle ($\theta$) along the path:

$$radius = \frac{a(1 - e^2)}{1 + e \cos(\theta)}$$
### Adding Patched conics
```


from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle

  
  
  

fig = plt.figure()

fig.set_dpi(100)

fig.set_size_inches(10, 10)

  

ax = plt.axes(xlim=(0, 30), ylim=(0, 30))

  
  

earth = Circle((5, -5), 0.75, fc='blue')

moon = Circle((5, -5), 0.2, fc='grey')

sun = Circle((5, -5), 2, fc='orange')

  

earth_mass = 10.0

moon_mass = 3.0

sun_mass = 100

  

sun_pos = np.array([15.0, 15.0])

earth_pos = np.array([15.0, 2])

moon_pos = np.array([15.0, 4])

  

sun_vel = np.array([0.0, 0.0])

earth_vel = np.array([0.08, 0.0])

moon_vel = np.array([0.04, 0.0])

  
  

earth_soi_circle = Circle((5, -5), 3, fc='grey', alpha=0.2)

moon_soi_circle = Circle((5, -5), 1, fc='grey', alpha=0.1)

  

GRAV_CONSTANT = 0.0001

  

def init():

ax.add_patch(earth_soi_circle)

ax.add_patch(moon_soi_circle)

ax.add_patch(earth)

ax.add_patch(moon)

ax.add_patch(sun)

  

return earth_soi_circle, moon_soi_circle, earth, moon, sun

  
  

def calculate_gravity(pos1, pos2, mass1, mass2):

displacement = pos1 - pos2

unit = displacement/np.linalg.norm(displacement)

gravitational_force = GRAV_CONSTANT * ((mass1 * mass2)/np.square(np.linalg.norm(displacement)))*unit

return gravitational_force

  
  

def calculate_orbit(pos1, pos2, mass, vec):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = GRAV_CONSTANT * mass

a = 1/(2/mod_r - mod_v_squared/mew)

e = (mod_v_squared - mew/mod_r) * displacement - (np.dot(displacement, vec))*vec / mew

def in_influence(pos1, pos2, influence):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

return (mod_r < influence.get_radius())

  

def animate(i):

global moon_pos

global moon_vel

global earth_pos

global earth_vel

  

earth_vel += calculate_gravity(sun_pos, earth_pos, earth_mass, sun_mass)

earth_pos += earth_vel

  

moon_vel += calculate_gravity(earth_pos, moon_pos, moon_mass, earth_mass)

moon_pos += moon_vel + earth_vel

  

earth_soi_circle.center = earth_pos

moon_soi_circle.center = moon_pos

sun.center = sun_pos

earth.center = earth_pos

moon.center = moon_pos

print(in_influence(earth_pos, moon_pos, earth_soi_circle))

  

return earth_soi_circle, moon_soi_circle, earth, moon, sun

  

anim = FuncAnimation(fig, animate,

init_func=init,

frames=360,

interval=20,

blit=True)

  

plt.show()

```

### Adding or minusing the velocity when it enters or leaves
```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle

  
  
  

fig = plt.figure()

fig.set_dpi(100)

fig.set_size_inches(10, 10)

  

ax = plt.axes(xlim=(0, 30), ylim=(0, 30))

  
  

earth = Circle((5, -5), 0.75, fc='blue')

moon = Circle((5, -5), 0.2, fc='grey')

sun = Circle((5, -5), 2, fc='orange')

  

earth_mass = 10.0

moon_mass = 3.0

sun_mass = 100

  

sun_pos = np.array([15.0, 15.0])

earth_pos = np.array([15.0, 2])

moon_pos = np.array([15.0, 4.5])

  

sun_vel = np.array([0.0, 0.0])

earth_vel = np.array([0.08, 0.0])

moon_vel = np.array([0.04, 0.0])

  
  

earth_soi_circle = Circle((5, -5), 5, fc='grey', alpha=0.2)

moon_soi_circle = Circle((5, -5), 1, fc='grey', alpha=0.1)

  

moon_in_earth_soi = True

moon_in_sun_soi = False

  

GRAV_CONSTANT = 0.0001

  

def init():

ax.add_patch(earth_soi_circle)

ax.add_patch(moon_soi_circle)

ax.add_patch(earth)

ax.add_patch(moon)

ax.add_patch(sun)

  

return earth_soi_circle, moon_soi_circle, earth, moon, sun

  
  

def calculate_gravity(pos1, pos2, mass1, mass2):

displacement = pos1 - pos2

unit = displacement/np.linalg.norm(displacement)

gravitational_force = GRAV_CONSTANT * ((mass1 * mass2)/np.square(np.linalg.norm(displacement)))*unit

return gravitational_force

  
  

def calculate_orbit(pos1, pos2, mass, vec):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = GRAV_CONSTANT * mass

a = 1/(2/mod_r - mod_v_squared/mew)

e = (mod_v_squared - mew/mod_r) * displacement - (np.dot(displacement, vec))*vec / mew

def in_influence(pos1, pos2, influence):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

return (mod_r < influence.get_radius())

  

def animate(i):

global moon_pos

global moon_vel

global earth_pos

global earth_vel

global moon_in_earth_soi

earth_vel += calculate_gravity(sun_pos, earth_pos, earth_mass, sun_mass)

earth_pos += earth_vel

  

if (in_influence(earth_pos, moon_pos, earth_soi_circle)):

if moon_in_earth_soi == False:

moon_vel -= earth_vel

moon_in_earth_soi = True

moon_vel += calculate_gravity(earth_pos, moon_pos, moon_mass, earth_mass)

moon_pos += moon_vel + earth_vel

else:

if moon_in_earth_soi == True:

moon_vel += earth_vel

moon_in_earth_soi = False

moon_vel += calculate_gravity(sun_pos, moon_pos, moon_mass, sun_mass)

moon_pos += moon_vel

  

earth_soi_circle.center = earth_pos

moon_soi_circle.center = moon_pos

sun.center = sun_pos

earth.center = earth_pos

moon.center = moon_pos

  

return earth_soi_circle, moon_soi_circle, earth, moon, sun

  

anim = FuncAnimation(fig, animate,

init_func=init,

frames=360,

interval=20,

blit=True)

  

try:

plt.show()

except KeyboardInterrupt:

pass
```

#### Generalising for all planets/bodies (back to issue where we need to minus or plus the relative velocities)
```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle

  
  
  

fig = plt.figure()

fig.set_dpi(100)

fig.set_size_inches(10, 10)

  

ax = plt.axes(xlim=(0, 30), ylim=(0, 30))

  
  

earth = Circle((5, -5), 0.75, fc='blue')

mars = Circle((5, -5), 0.5, fc='blue')

moon = Circle((5, -5), 0.2, fc='grey')

sun = Circle((5, -5), 2, fc='orange')

  

names = ["earth", "moon", "mars"]

bodies = [earth, moon, mars]

body_masses = [10, 3, 4]

  

earth_mass = 12.0

moon_mass = 3.0

sun_mass = 100

  

sun_pos = np.array([15.0, 15.0])

earth_pos = np.array([15.0, 2])

moon_pos = np.array([15.0, 4.5])

mars_pos = np.array([15.0, 24])

  
  

body_pos = [earth_pos, moon_pos, mars_pos]

  

sun_vel = np.array([0.0, 0.0])

earth_vel = np.array([0.08, 0.0])

moon_vel = np.array([-0.06, 0.0])

mars_vel = np.array([0.06, 0.0])

bod_vel = [earth_vel, moon_vel, mars_vel]

  

earth_soi_circle = Circle((5, -5), 5, fc='grey', alpha=0.2)

mars_soi_circle = Circle((5, -5), 2, fc='grey', alpha=0.2)

moon_soi_circle = Circle((5, -5), 1, fc='grey', alpha=0.1)

  

body_soi = [earth_soi_circle, moon_soi_circle, mars_soi_circle]

  

moon_in_earth_soi = True

moon_in_sun_soi = False

  

current_sois = [-1, -1, -1]

  

GRAV_CONSTANT = 0.0001

  
  
  
  

def init():

ax.add_patch(earth_soi_circle)

ax.add_patch(moon_soi_circle)

ax.add_patch(mars_soi_circle)

ax.add_patch(earth)

ax.add_patch(mars)

ax.add_patch(moon)

ax.add_patch(sun)

  

return earth_soi_circle, mars_soi_circle, moon_soi_circle, earth, mars, moon, sun

  
  

def calculate_gravity(pos1, pos2, mass1, mass2):

displacement = pos1 - pos2

unit = displacement/np.linalg.norm(displacement)

gravitational_force = GRAV_CONSTANT * ((mass1 * mass2)/np.square(np.linalg.norm(displacement)))*unit

return gravitational_force

  
  

def calculate_orbit(pos1, pos2, mass, vec):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = GRAV_CONSTANT * mass

a = 1/(2/mod_r - mod_v_squared/mew)

e = (mod_v_squared - mew/mod_r) * displacement - (np.dot(displacement, vec))*vec / mew

def in_influence(pos1, pos2, influence):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

return (mod_r < influence.get_radius())

  

def get_influence(pos, pos_list, soi_list):

for i in range(0, len(soi_list)):

if in_influence(pos_list[i], pos, soi_list[i]):

return i

return -1

  

def animate(j):

global moon_pos

global moon_vel

global earth_pos

global earth_vel

global moon_in_earth_soi

  

# for each planet calculate which sphere of influence you are in (default to sun)

for i in range(0, len(bodies)):

temp = get_influence(body_pos[i], body_pos, body_soi)

  

# if in certain sphere then calculate relative to that

if names[i] != names[temp]:

bod_vel[i] += calculate_gravity(body_pos[temp], body_pos[i], body_masses[i], body_masses[temp])

body_pos[i] += bod_vel[i] + bod_vel[temp]

# else calculate relative to sun

else:

print(names[i])

bod_vel[i] += calculate_gravity(sun_pos, body_pos[i], body_masses[i], sun_mass)

body_pos[i] += bod_vel[i]

  

earth_soi_circle.center = body_pos[0]

moon_soi_circle.center = body_pos[1]

mars_soi_circle.center = body_pos[2]

  

sun.center = sun_pos

earth.center = body_pos[0]

moon.center = body_pos[1]

mars.center = body_pos[2]

  

return earth_soi_circle, mars_soi_circle, moon_soi_circle, earth, mars, moon, sun

  

anim = FuncAnimation(fig, animate,

init_func=init,

frames=360,

interval=20,

blit=True)

  

try:

plt.show()

except KeyboardInterrupt:

pass
```


#### do sun gravity first and then add any local gravity

```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle

  

class OrbitalSimulation:

def __init__(self):

self.fig = plt.figure()

self.fig.set_dpi(100)

self.fig.set_size_inches(10, 10)

self.ax = plt.axes(xlim=(0, 100), ylim=(0, 100))

self.ax.set_facecolor('black')

self.earth = Circle((5, -5), 0.75, fc='blue')

self.mars = Circle((5, -5), 0.5, fc='red')

self.moon = Circle((5, -5), 0.2, fc='grey')

self.sun = Circle((5, -5), 2, fc='orange')

  

self.names = ["earth", "moon", "mars"]

self.bodies = [self.earth, self.moon, self.mars]

self.body_masses = [10, 0.1, 4]

  

self.sun_mass = 80

  

self.sun_pos = np.array([50.0, 50.0])

self.earth_pos = np.array([50.0, 68])

self.moon_pos = np.array([50.0, 71])

self.mars_pos = np.array([50.0, 90])

  

self.body_pos = [self.earth_pos, self.moon_pos, self.mars_pos]

  

self.sun_vel = np.array([0.0, 0.0])

self.earth_vel = np.array([0.22, 0.0])

self.moon_vel = np.array([0.36, 0.0])

self.mars_vel = np.array([0.13, 0.0])

self.bod_vel = [self.earth_vel, self.moon_vel, self.mars_vel]

  

self.earth_soi_circle = Circle((5, -5), 4.35, fc='grey', alpha=0.2)

self.mars_soi_circle = Circle((5, -5), 3, fc='grey', alpha=0.2)

self.moon_soi_circle = Circle((5, -5), 0.1, fc='grey', alpha=0.1)

  

self.body_soi = [self.earth_soi_circle, self.moon_soi_circle, self.mars_soi_circle]

  

self.moon_in_earth_soi = True

self.moon_in_sun_soi = False

self.current_sois = [-1, -1, -1]

self.GRAV_CONSTANT = 0.01

  

self.dt = 0.7

  

def init(self):

self.ax.add_patch(self.earth_soi_circle)

self.ax.add_patch(self.moon_soi_circle)

self.ax.add_patch(self.mars_soi_circle)

self.ax.add_patch(self.earth)

self.ax.add_patch(self.mars)

self.ax.add_patch(self.moon)

self.ax.add_patch(self.sun)

return (self.earth_soi_circle, self.mars_soi_circle, self.moon_soi_circle,

self.earth, self.mars, self.moon, self.sun)

  

def calculate_gravity(self, pos1, pos2, mass):

displacement = pos1 - pos2

r = np.linalg.norm(displacement)

unit = displacement / r

gravity_force = self.GRAV_CONSTANT * (mass / (r**2)) * unit

return gravity_force

  

def calculate_orbit(self, pos1, pos2, mass, vec):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = self.GRAV_CONSTANT * mass

a = 1 / (2 / mod_r - mod_v_squared / mew)

e = (mod_v_squared - mew / mod_r) * displacement - (np.dot(displacement, vec)) * vec / mew

def in_influence(self, pos1, pos2, influence):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

return (mod_r < influence.get_radius())

def get_influence(self, pos, pos_list, soi_list, index):

for i in range(0, len(soi_list)):

if i != index:

if self.in_influence(pos_list[i], pos, soi_list[i]):

return i

return -1

def animate(self, j):

for i in range(0, len(self.bodies)):

self.bod_vel[i] += self.calculate_gravity(self.sun_pos, self.body_pos[i], self.sun_mass) * self.dt

temp = self.get_influence(self.body_pos[i], self.body_pos, self.body_soi, i)

if temp != -1:

self.bod_vel[i] += self.calculate_gravity(self.body_pos[temp], self.body_pos[i], self.body_masses[temp]) * self.dt

self.body_pos[i] += self.bod_vel[i] * self.dt

  

self.earth_soi_circle.center = self.body_pos[0]

self.moon_soi_circle.center = self.body_pos[1]

self.mars_soi_circle.center = self.body_pos[2]

  

self.sun.center = self.sun_pos

self.earth.center = self.body_pos[0]

self.moon.center = self.body_pos[1]

self.mars.center = self.body_pos[2]

  

return (self.earth_soi_circle, self.mars_soi_circle, self.moon_soi_circle,

self.earth, self.mars, self.moon, self.sun)

  

def run(self):

self.anim = FuncAnimation(self.fig, self.animate,

init_func=self.init,

frames=360,

interval=20,

blit=True)

try:

plt.show()

except KeyboardInterrupt:

pass

  

if __name__ == "__main__":

sim = OrbitalSimulation()

sim.run()
```

#### Adding buttons and sliders

https://matplotlib.org/stable/gallery/widgets/slider_demo.html

#### And orbit lines 
```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle

from matplotlib.widgets import Button, Slider

  
  

class OrbitalSimulation:

def __init__(self):

self.fig = plt.figure()

self.fig.set_dpi(100)

self.fig.set_size_inches(10, 10)

self.ax = plt.axes([0.1, 0.25, 0.8, 0.70], xlim=(0, 100), ylim=(0, 100)) # type: ignore

# self.ax.set_facecolor('black')

self.earth = Circle((5, -5), 0.75, fc='blue')

self.mars = Circle((5, -5), 0.5, fc='red')

self.moon = Circle((5, -5), 0.2, fc='grey')

self.sun = Circle((5, -5), 2, fc='orange')

  

self.names = ["earth", "moon", "mars"]

self.bodies = [self.earth, self.moon, self.mars]

self.body_masses = [10, 0.1, 4]

  

self.sun_mass = 80

  

self.sun_pos = np.array([50.0, 50.0])

self.earth_pos = np.array([50.0, 68])

self.moon_pos = np.array([50.0, 71])

self.mars_pos = np.array([50.0, 90])

  

self.body_pos = [self.earth_pos, self.moon_pos, self.mars_pos]

  

self.sun_vel = np.array([0.0, 0.0])

self.earth_vel = np.array([0.215, 0.0])

self.moon_vel = np.array([0.36, 0.0])

self.mars_vel = np.array([0.142, 0.0])

self.bod_vel = [self.earth_vel, self.moon_vel, self.mars_vel]

  

self.earth_soi_circle = Circle((5, -5), 4.35, fc='grey', alpha=0.2)

self.mars_soi_circle = Circle((5, -5), 3, fc='grey', alpha=0.2)

self.moon_soi_circle = Circle((5, -5), 0.1, fc='grey', alpha=0.1)

  

self.body_soi = [self.earth_soi_circle, self.moon_soi_circle, self.mars_soi_circle]

self.orbit_lines = []

for i in range(0, len(self.bodies)):

line, = self.ax.plot([], [], 'r--', linewidth=1.5, label="Orbit Path")

self.orbit_lines.append(line)

  

self.moon_in_earth_soi = True

self.moon_in_sun_soi = False

self.GRAV_CONSTANT = 0.01

  

self.dt = 0.7

  

self.setup_widgets()

  
  

def setup_widgets(self):

ax_slider = plt.axes([0.15, 0.08, 0.2, 0.03]) # type: ignore

self.slider = Slider(ax_slider, 'Time', 0, 3, valinit=0.7, valfmt='%1.3f')

self.slider.on_changed(self.update_dt)

  

resetax = plt.axes([0.15, 0.15, 0.1, 0.04]) # type: ignore

self.button = Button(resetax, 'Reset', hovercolor='0.775')

self.button.on_clicked(self.reset)

  

def update_dt(self, n):

self.dt = n

  

def reset(self, event):

self.slider.reset()

  

def init(self):

self.ax.add_patch(self.earth_soi_circle)

self.ax.add_patch(self.moon_soi_circle)

self.ax.add_patch(self.mars_soi_circle)

self.ax.add_patch(self.earth)

self.ax.add_patch(self.mars)

self.ax.add_patch(self.moon)

self.ax.add_patch(self.sun)

return (self.earth_soi_circle, self.mars_soi_circle, self.moon_soi_circle,

self.earth, self.mars, self.moon, self.sun)

  

def calculate_gravity(self, pos1, pos2, mass):

displacement = pos1 - pos2

r = np.linalg.norm(displacement)

unit = displacement / r

gravity_force = self.GRAV_CONSTANT * (mass / (r**2)) * unit

return gravity_force

  

def calculate_orbit(self, pos1, pos2, mass, vec):

displacement = pos1 - pos2 # Vector from central body to object

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = self.GRAV_CONSTANT * mass

a = 1 / (2 / mod_r - mod_v_squared / mew)

e_vec = ((mod_v_squared - mew / mod_r) * displacement - np.dot(displacement, vec) * vec) / mew

e = np.linalg.norm(e_vec)

omega = np.arctan2(e_vec[1], e_vec[0])

theta = np.linspace(0, 2 * np.pi, 200)

r_orbit = (a * (1 - e**2)) / (1 + e * np.cos(theta))

x_local = r_orbit * np.cos(theta)

y_local = r_orbit * np.sin(theta)

x_world = pos2[0] + (x_local * np.cos(omega) - y_local * np.sin(omega))

y_world = pos2[1] + (x_local * np.sin(omega) + y_local * np.cos(omega))

return x_world, y_world

def in_influence(self, pos1, pos2, influence):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

return (mod_r < influence.get_radius())

def get_influence(self, pos, pos_list, soi_list, index):

for i in range(0, len(soi_list)):

if i != index:

if self.in_influence(pos_list[i], pos, soi_list[i]):

return i

return -1

def animate(self, j):

for i in range(0, len(self.bodies)):

self.bod_vel[i] += self.calculate_gravity(self.sun_pos, self.body_pos[i], self.sun_mass) * self.dt

temp = self.get_influence(self.body_pos[i], self.body_pos, self.body_soi, i)

if temp != -1:

self.bod_vel[i] += self.calculate_gravity(self.body_pos[temp], self.body_pos[i], self.body_masses[temp]) * self.dt

self.body_pos[i] += self.bod_vel[i] * self.dt

  

self.earth_soi_circle.center = self.body_pos[0]

self.moon_soi_circle.center = self.body_pos[1]

self.mars_soi_circle.center = self.body_pos[2]

  

self.sun.center = self.sun_pos

self.earth.center = self.body_pos[0]

self.moon.center = self.body_pos[1]

self.mars.center = self.body_pos[2]

  

for i in range(0, len(self.bodies)):

x_pts, y_pts = self.calculate_orbit(self.body_pos[i], self.sun_pos, self.sun_mass, self.bod_vel[i])

self.orbit_lines[i].set_data(x_pts, y_pts)

  

return (self.earth_soi_circle, self.mars_soi_circle, self.moon_soi_circle,

*self.bodies, self.sun, self.orbit_lines[0], self.orbit_lines[2])

  

def run(self):

self.anim = FuncAnimation(self.fig, self.animate,

init_func=self.init,

frames=360,

interval=20,

blit=True)

try:

plt.show()

except KeyboardInterrupt:

pass

  

if __name__ == "__main__":

sim = OrbitalSimulation()

sim.run()
```


#### Rewritten with dictionaries

```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle

from matplotlib.widgets import Button, Slider

  
  

class OrbitalSimulation:

def __init__(self):

self.fig = plt.figure()

self.fig.set_dpi(100)

self.fig.set_size_inches(10, 10)

self.ax = plt.axes([0.1, 0.25, 0.8, 0.70], xlim=(0, 100), ylim=(0, 100)) # type: ignore

# self.ax.set_facecolor('black')

  

# Planet dict: Circle, Mass, Position, Velocity, SOI Circle, Orbit

self.planet = {

"jupiter": [Circle((5, -5), 1.5, fc='brown'), 20,np.array([50.0, 10.0]), np.array([0.115, 0.0]), Circle((5, -5), 8.0, fc='grey', alpha=0.15)],

"earth": [Circle((5, -5), 0.75, fc='blue'), 10,np.array([50.0, 68.0]), np.array([0.215, 0.0]), Circle((5, -5), 4.35, fc='grey', alpha=0.15)],

"mars": [Circle((5, -5), 0.5, fc='red'), 4, np.array([50.0, 90.0]), np.array([0.142, 0.0]), Circle((5, -5), 3.0, fc='grey', alpha=0.15)],

"moon": [Circle((5, -5), 0.2, fc='grey'), 0.1,np.array([50.0, 71.0]), np.array([0.360, 0.0]), Circle((5, -5), 0.5, fc='grey', alpha=0.05)]

}

  
  

# Sun won't change

self.sun = Circle((5, -5), 2, fc='orange')

self.sun_mass = 80

self.sun_pos = np.array([50.0, 50.0])

  
  

self.orbit_lines = []

for _, data in self.planet.items():

line, = self.ax.plot([], [], 'r--', linewidth=1.5, label="Orbit Path")

data.append(line)

  
  

self.GRAV_CONSTANT = 0.01

self.dt = 0.7

self.setup_widgets()

  
  

def setup_widgets(self):

ax_slider = plt.axes([0.15, 0.08, 0.2, 0.03]) # type: ignore

self.slider = Slider(ax_slider, 'Time', 0, 3, valinit=0.7, valfmt='%1.3f')

self.slider.on_changed(self.update_dt)

  

resetax = plt.axes([0.15, 0.15, 0.1, 0.04]) # type: ignore

self.button = Button(resetax, 'Reset', hovercolor='0.775')

self.button.on_clicked(self.reset)

  

def update_dt(self, n):

self.dt = n

  

def reset(self, event):

self.slider.reset()

  

def init(self):

return_values = []

for _, data in self.planet.items():

self.ax.add_patch(data[4])

self.ax.add_patch(data[0])

return_values.extend([data[4], data[0]])

self.ax.add_patch(self.sun)

return_values.append(self.sun)

return tuple(return_values)

  

def calculate_gravity(self, pos1, pos2, mass):

displacement = pos1 - pos2

r = np.linalg.norm(displacement)

unit = displacement / r

gravity_force = self.GRAV_CONSTANT * (mass / (r**2)) * unit

return gravity_force

  

def calculate_orbit(self, pos1, pos2, mass, vec):

displacement = pos1 - pos2 # Vector from central body to object

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = self.GRAV_CONSTANT * mass

a = 1 / (2 / mod_r - mod_v_squared / mew)

e_vec = ((mod_v_squared - mew / mod_r) * displacement - np.dot(displacement, vec) * vec) / mew

e = np.linalg.norm(e_vec)

omega = np.arctan2(e_vec[1], e_vec[0])

theta = np.linspace(0, 2 * np.pi, 200)

r_orbit = (a * (1 - e**2)) / (1 + e * np.cos(theta))

x_local = r_orbit * np.cos(theta)

y_local = r_orbit * np.sin(theta)

x_world = pos2[0] + (x_local * np.cos(omega) - y_local * np.sin(omega))

y_world = pos2[1] + (x_local * np.sin(omega) + y_local * np.cos(omega))

return x_world, y_world

def in_influence(self, pos1, pos2, radius):

return np.linalg.norm(pos1 - pos2) < radius

def get_influence(self, current_name, current_pos):

for name, data in self.planet.items():

if name != current_name:

soi_radius = data[4].get_radius()

if self.in_influence(data[2], current_pos, soi_radius):

return name

return "sun"

def animate(self, j):

updated_artists = []

parents = {}

for name, data in self.planet.items():

data[3] += self.calculate_gravity(self.sun_pos, data[2], self.sun_mass) * self.dt

parent = self.get_influence(name, data[2])

parents[name] = parent

if parent != "sun":

parent_data = self.planet[parent]

data[3] += self.calculate_gravity(parent_data[2], data[2], parent_data[1]) * self.dt

data[2] += data[3] * self.dt

  

self.sun.center = self.sun_pos

updated_artists.append(self.sun)

  

self.sun.center = self.sun_pos

  

for name, data in self.planet.items():

data[0].center = data[2]

data[4].center = data[2]

updated_artists.extend([data[0], data[4]])

  

x_pts, y_pts = self.calculate_orbit(data[2], self.sun_pos, self.sun_mass, data[3])

data[5].set_data(x_pts, y_pts)

if name != "moon":

updated_artists.append(data[5])

  

return tuple(updated_artists)

  

def run(self):

self.anim = FuncAnimation(self.fig, self.animate,

init_func=self.init,

frames=360,

interval=20,

blit=True)

try:

plt.show()

except KeyboardInterrupt:

pass

  

if __name__ == "__main__":

sim = OrbitalSimulation()

sim.run()
```


#### Zoom and moon orbit line fix
https://www.geeksforgeeks.org/python/matplotlib-plot-zooming-with-scroll-wheel/
```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle

from matplotlib.widgets import Button, Slider

from mpl_interactions import ioff, panhandler, zoom_factory

  
  

class OrbitalSimulation:

def __init__(self):

with plt.ioff():

self.fig = plt.figure()

self.fig.set_dpi(100)

self.fig.set_size_inches(10, 10

)

with plt.ioff():

self.ax = plt.axes([0.1, 0.25, 0.8, 0.70], xlim=(0, 100), ylim=(0, 100)) # type: ignore

# self.ax.set_facecolor('black')

  

# Planet dict: Circle, Mass, Position, Velocity, SOI Circle, Orbit

self.planet = {

"jupiter": [Circle((5, -5), 1.5, fc='brown'), 20,np.array([50.0, 0.0]), np.array([0.15, 0.0]), Circle((5, -5), 8.0, fc='grey', alpha=0.15)],

"earth": [Circle((5, -5), 0.75, fc='blue'), 10,np.array([50.0, 68.0]), np.array([0.215, 0.0]), Circle((5, -5), 4.35, fc='grey', alpha=0.15)],

"mars": [Circle((5, -5), 0.5, fc='red'), 4, np.array([50.0, 90.0]), np.array([0.142, 0.0]), Circle((5, -5), 3.0, fc='grey', alpha=0.15)],

"moon": [Circle((5, -5), 0.2, fc='grey'), 1,np.array([50.0, 71.0]), np.array([0.35, 0.0]), Circle((5, -5), 0.5, fc='grey', alpha=0.05)]

}

  
  

# Sun won't change

self.sun = Circle((5, -5), 2, fc='orange')

self.sun_mass = 80

self.sun_pos = np.array([50.0, 50.0])

  
  

self.orbit_lines = []

for _, data in self.planet.items():

line, = self.ax.plot([], [], 'r--', linewidth=1.5, label="Orbit Path")

data.append(line)

  
  

self.GRAV_CONSTANT = 0.01

self.dt = 0.7

self.setup_widgets()

disconnect_zoom = zoom_factory(self.ax)

pan_handler = panhandler(self.fig)

  
  
  

def setup_widgets(self):

ax_slider = plt.axes([0.15, 0.08, 0.2, 0.03]) # type: ignore

self.slider = Slider(ax_slider, 'Time', 0, 3, valinit=0.7, valfmt='%1.3f')

self.slider.on_changed(self.update_dt)

  

resetax = plt.axes([0.15, 0.15, 0.1, 0.04]) # type: ignore

self.button = Button(resetax, 'Reset', hovercolor='0.775')

self.button.on_clicked(self.reset)

  

def update_dt(self, n):

self.dt = n

  

def reset(self, event):

self.slider.reset()

  

def init(self):

return_values = []

for _, data in self.planet.items():

self.ax.add_patch(data[4])

self.ax.add_patch(data[0])

return_values.extend([data[4], data[0]])

self.ax.add_patch(self.sun)

return_values.append(self.sun)

return tuple(return_values)

  

def calculate_gravity(self, pos1, pos2, mass):

displacement = pos1 - pos2

r = np.linalg.norm(displacement)

unit = displacement / r

gravity_force = self.GRAV_CONSTANT * (mass / (r**2)) * unit

return gravity_force

  

def calculate_orbit(self, pos1, pos2, mass, vec):

displacement = pos1 - pos2 # Vector from central body to object

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = self.GRAV_CONSTANT * mass

a = 1 / (2 / mod_r - mod_v_squared / mew)

e_vec = ((mod_v_squared - mew / mod_r) * displacement - np.dot(displacement, vec) * vec) / mew

e = np.linalg.norm(e_vec)

omega = np.arctan2(e_vec[1], e_vec[0])

theta = np.linspace(0, 2 * np.pi, 200)

r_orbit = (a * (1 - e**2)) / (1 + e * np.cos(theta))

x_local = r_orbit * np.cos(theta)

y_local = r_orbit * np.sin(theta)

x_world = pos2[0] + (x_local * np.cos(omega) - y_local * np.sin(omega))

y_world = pos2[1] + (x_local * np.sin(omega) + y_local * np.cos(omega))

return x_world, y_world

def in_influence(self, pos1, pos2, radius):

return np.linalg.norm(pos1 - pos2) < radius

def get_influence(self, current_name, current_pos):

for name, data in self.planet.items():

if name != current_name:

soi_radius = data[4].get_radius()

if self.in_influence(data[2], current_pos, soi_radius):

return name

return "sun"

def animate(self, j):

updated_artists = []

parents = {}

for name, data in self.planet.items():

data[3] += self.calculate_gravity(self.sun_pos, data[2], self.sun_mass) * self.dt

parent = self.get_influence(name, data[2])

parents[name] = parent

if parent != "sun":

parent_data = self.planet[parent]

data[3] += self.calculate_gravity(parent_data[2], data[2], parent_data[1]) * self.dt

data[2] += data[3] * self.dt

  

self.sun.center = self.sun_pos

updated_artists.append(self.sun)

  

self.sun.center = self.sun_pos

  

for name, data in self.planet.items():

data[0].center = data[2]

data[4].center = data[2]

updated_artists.extend([data[0], data[4]])

if parents[name] == "sun":

x_pts, y_pts = self.calculate_orbit(data[2], self.sun_pos, self.sun_mass, data[3])

else:

parent_data = self.planet[parents[name]]

parent_pos = parent_data[2]

parent_mass = parent_data[1]

parent_vel = parent_data[3]

  

rel_pos = data[2] - parent_pos

rel_vel = data[3] - parent_vel

  

x_local, y_local = self.calculate_orbit(rel_pos, np.array([0.0, 0.0]), parent_mass, rel_vel)

x_pts = x_local + parent_pos[0]

y_pts = y_local + parent_pos[1]

  

data[5].set_data(x_pts, y_pts)

updated_artists.append(data[5])

  

return tuple(updated_artists)

  

def run(self):

self.anim = FuncAnimation(self.fig, self.animate,

init_func=self.init,

frames=360,

interval=20,

blit=True)

try:

plt.show()

except KeyboardInterrupt:

pass

  

if __name__ == "__main__":

sim = OrbitalSimulation()

sim.run()
```


#### Spawn rocket logic

```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle, Rectangle

from matplotlib.widgets import Button, Slider

from mpl_interactions import ioff, panhandler, zoom_factory

  
  

class OrbitalSimulation:

def __init__(self):

with plt.ioff():

self.fig = plt.figure()

self.fig.set_dpi(100)

self.fig.set_size_inches(10, 10

)

with plt.ioff():

self.ax = plt.axes([0.1, 0.25, 0.8, 0.70], xlim=(0, 100), ylim=(0, 100)) # type: ignore

self.ax.set_facecolor('black')

  

# Planet dict: Circle, Mass, Position, Velocity, SOI Circle, Orbit

self.bodies = {

"jupiter": [Circle((5, -5), 1.5, fc='brown', zorder=3), 20,np.array([50.0, 0.0]), np.array([0.15, 0.0]), Circle((5, -5), 8.0, fc='grey', alpha=0.15, zorder=2)],

"earth": [Circle((5, -5), 0.75, fc='blue', zorder=3), 10,np.array([50.0, 68.0]), np.array([0.215, 0.0]), Circle((5, -5), 4.35, fc='grey', alpha=0.15, zorder=2)],

"mars": [Circle((5, -5), 0.5, fc='red', zorder=3), 4, np.array([50.0, 90.0]), np.array([0.142, 0.0]), Circle((5, -5), 3.0, fc='grey', alpha=0.15,zorder=2)],

"moon": [Circle((5, -5), 0.2, fc='grey', zorder=3), 3 ,np.array([50.0, 71.0]), np.array([0.38, 0.0]), Circle((5, -5), 0.5, fc='grey', alpha=0.05,zorder=2)]

}

  
  

# Sun won't change

self.sun = Circle((5, -5), 2, fc='orange')

self.sun_mass = 80

self.sun_pos = np.array([50.0, 50.0])

  
  

self.orbit_lines = []

for _, data in self.bodies.items():

line, = self.ax.plot([], [], 'r--', linewidth=1.5, label="Orbit Path", zorder=1)

data.append(line)

  
  

self.GRAV_CONSTANT = 0.01

self.dt = 0

  

self.setup_widgets()

self.disconnect_zoom = zoom_factory(self.ax)

self.pan_handler = panhandler(self.fig, button=1)

  
  
  

def setup_widgets(self):

ax_slider = plt.axes([0.15, 0.08, 0.2, 0.03]) # type: ignore

self.slider = Slider(ax_slider, 'Time', 0, 3, valinit=0.7, valfmt='%1.3f')

self.slider.on_changed(self.update_dt)

  

pause_sim = plt.axes([0.15, 0.15, 0.1, 0.04]) # type: ignore

self.pause_button = Button(pause_sim, 'Pause', hovercolor='0.775')

self.pause_button.on_clicked(self.pause)

  

play_sim = plt.axes([0.25, 0.15, 0.1, 0.04]) # type: ignore

self.button = Button(play_sim, 'Play', hovercolor='0.775')

self.button.on_clicked(self.play)

  

reset_time = plt.axes([0.35, 0.15, 0.1, 0.04]) # type: ignore

self.reset_button = Button(reset_time, 'Reset', hovercolor='0.775')

self.reset_button.on_clicked(self.reset)

  

spawn = plt.axes([0.60, 0.15, 0.1, 0.04]) # type: ignore

self.spawn_button = Button(spawn, 'Spawn', hovercolor='0.775')

self.spawn_button.on_clicked(self.spawn_rocket)

launch = plt.axes([0.75, 0.15, 0.1, 0.04]) # type: ignore

self.launch_button = Button(launch, 'Launch', hovercolor='0.775')

self.launch_button.on_clicked(self.launch_rocket)

  
  

def update_dt(self, n):

self.dt = n

  

def reset(self, event):

self.slider.reset()

  

def pause(self, event):

self.dt = 0

  

def play(self, event):

self.dt = self.slider.val

  

def spawn_rocket(self, event):

line, = self.ax.plot([], [], 'r--', linewidth=1.5, label="Orbit Path", zorder=1)

self.bodies["Rocket"] = [Circle((5, -5), 0.1, fc='grey', zorder=3), 0.0001 ,np.array([50.0, 92.0]), np.array([0.28, 0.0]), Circle((5, -5), 0, fc='grey', alpha=0,zorder=2), line]

self.ax.add_patch(self.bodies["Rocket"][4])

self.ax.add_patch(self.bodies["Rocket"][0])

  

def launch_rocket(self, event):

try:

self.bodies["Rocket"][3] += np.array([0.06, 0])

except:

print("no rocket")

  

def init(self):

for _, data in self.bodies.items():

self.ax.add_patch(data[4])

self.ax.add_patch(data[0])

self.ax.add_patch(self.sun)

return []

  

def calculate_gravity(self, pos1, pos2, mass):

displacement = pos1 - pos2

r = np.linalg.norm(displacement)

if r != 0:

unit = displacement / r

else:

unit = 0

gravity_force = self.GRAV_CONSTANT * (mass / (r**2)) * unit

return gravity_force

  

def calculate_orbit(self, pos1, pos2, mass, vec):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = self.GRAV_CONSTANT * mass

a = 1 / (2 / mod_r - mod_v_squared / mew)

e_vec = ((mod_v_squared - mew / mod_r) * displacement - np.dot(displacement, vec) * vec) / mew

e = np.linalg.norm(e_vec)

omega = np.arctan2(e_vec[1], e_vec[0])

theta = np.linspace(0, 2 * np.pi, 200)

r_orbit = (a * (1 - e**2)) / (1 + e * np.cos(theta))

x_local = r_orbit * np.cos(theta)

y_local = r_orbit * np.sin(theta)

x_world = pos2[0] + (x_local * np.cos(omega) - y_local * np.sin(omega))

y_world = pos2[1] + (x_local * np.sin(omega) + y_local * np.cos(omega))

return x_world, y_world

def in_influence(self, pos1, pos2, radius):

return np.linalg.norm(pos1 - pos2) < radius

def get_influence(self, current_name, current_pos):

for name, data in self.bodies.items():

if name != current_name:

soi_radius = data[4].get_radius()

if self.in_influence(current_pos, data[2], soi_radius):

return name

return "sun"

def animate(self, j):

parents = {}

for name, data in self.bodies.items():

data[3] += self.calculate_gravity(self.sun_pos, data[2], self.sun_mass) * self.dt

parent = self.get_influence(name, data[2])

parents[name] = parent

if parent != "sun":

parent_data = self.bodies[parent]

data[3] += self.calculate_gravity(parent_data[2], data[2], parent_data[1]) * self.dt

data[2] += data[3] * self.dt

  

self.sun.center = self.sun_pos

  

for name, data in self.bodies.items():

data[0].center = data[2]

data[4].center = data[2]

if parents[name] == "sun":

x_pts, y_pts = self.calculate_orbit(data[2], self.sun_pos, self.sun_mass, data[3])

else:

parent_data = self.bodies[parents[name]]

parent_pos = parent_data[2]

parent_mass = parent_data[1]

parent_vel = parent_data[3]

  

rel_pos = data[2] - parent_pos

rel_vel = data[3] - parent_vel

  

x_local, y_local = self.calculate_orbit(rel_pos, np.array([0.0, 0.0]), parent_mass, rel_vel)

x_pts = x_local + parent_pos[0]

y_pts = y_local + parent_pos[1]

  

data[5].set_data(x_pts, y_pts)

  

return []

  

def run(self):

self.anim = FuncAnimation(self.fig, self.animate,

init_func=self.init,

frames=360,

interval=20,

blit=False)

try:

plt.show()

except KeyboardInterrupt:

pass

  

if __name__ == "__main__":

sim = OrbitalSimulation()

sim.run()
```


#### Rocket transfer and wobble fix 
```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle, Rectangle

from matplotlib.widgets import Button, Slider

from mpl_interactions import ioff, panhandler, zoom_factory

import copy

  
  

class OrbitalSimulation:

def __init__(self):

with plt.ioff():

self.fig = plt.figure()

self.fig.set_dpi(100)

self.fig.set_size_inches(10, 10

)

with plt.ioff():

self.ax = plt.axes([0.1, 0.25, 0.8, 0.70], xlim=(0, 300), ylim=(0, 300)) # type: ignore

self.ax.set_facecolor('black')

  

# Sun won't change

self.sun = Circle((5, -5), 4, fc='orange')

self.sun_mass = 250

self.sun_pos = np.array([150.0, 150.0])

  

# Planet dict: Circle, Mass, Position, Velocity, SOI Circle, Orbit

self.bodies = {

#"mercury": [Circle((5, -5), 0.4, fc='darkgrey', zorder=3), 2, np.array([150.0, 175.0]), np.array([0.316, 0.0]), Circle((5, -5), 1.5, fc='grey', alpha=0.15, zorder=2)],

#"venus": [Circle((5, -5), 0.7, fc='gold', zorder=3), 6, np.array([150.0, 195.0]), np.array([0.235, 0.0]), Circle((5, -5), 3.5, fc='grey', alpha=0.15, zorder=2)],

"earth": [Circle((5, -5), 0.75, fc='blue', zorder=3), 10, np.array([150.0, 220.0]), np.array([0.195, 0.0]), Circle((5, -5), 6.5, fc='grey', alpha=0.15, zorder=2)],

"moon": [Circle((5, -5), 0.2, fc='grey', zorder=3), 1, np.array([150.0, 224.5]), np.array([0.345, 0.0]), Circle((5, -5), 0.8, fc='grey', alpha=0.05, zorder=2)],

"mars": [Circle((5, -5), 0.5, fc='red', zorder=3), 4, np.array([150.0, 275.0]), np.array([0.144, 0.0]), Circle((5, -5), 4.0, fc='grey', alpha=0.15, zorder=2)],

#"jupiter": [Circle((5, -5), 1.8, fc='brown', zorder=3), 35, np.array([150.0, 80.0]), np.array([-0.188, 0.0]), Circle((5, -5), 15.0, fc='grey', alpha=0.15, zorder=2)],

#"saturn": [Circle((5, -5), 1.4, fc='purple', zorder=3), 20, np.array([150.0, 10.0]), np.array([-0.133, 0.0]), Circle((5, -5), 12.0, fc='grey', alpha=0.15, zorder=2)]

}

  

self.init_copy = copy.deepcopy(self.bodies)

  
  
  
  

self.orbit_lines = []

for _, data in self.bodies.items():

line, = self.ax.plot([], [], 'r--', linewidth=0.9, label="Orbit Path", zorder=1)

  

data.append(line)

  
  

self.GRAV_CONSTANT = 0.01

self.dt = 0

self.step_size = 0.05

  
  

self.setup_widgets()

self.disconnect_zoom = zoom_factory(self.ax)

self.pan_handler = panhandler(self.fig, button=1)

  
  
  

def setup_widgets(self):

ax_slider = plt.axes([0.15, 0.08, 0.2, 0.03]) # type: ignore

self.slider = Slider(ax_slider, 'Time', 0, 5, valinit=0.7, valfmt='%1.3f')

self.slider.on_changed(self.update_dt)

  

pause_sim = plt.axes([0.15, 0.15, 0.1, 0.04]) # type: ignore

self.pause_button = Button(pause_sim, 'Pause', hovercolor='0.775')

self.pause_button.on_clicked(self.pause)

  

play_sim = plt.axes([0.25, 0.15, 0.1, 0.04]) # type: ignore

self.button = Button(play_sim, 'Play', hovercolor='0.775')

self.button.on_clicked(self.play)

  

reset_time = plt.axes([0.35, 0.15, 0.1, 0.04]) # type: ignore

self.reset_button = Button(reset_time, 'Reset', hovercolor='0.775')

self.reset_button.on_clicked(self.reset)

  

reset_simulation = plt.axes([0.65, 0.04, 0.15, 0.04]) # type: ignore

self.reset_sim_button = Button(reset_simulation, 'Reset Simulation', hovercolor='0.775')

self.reset_sim_button.on_clicked(self.reset_sim)

  

spawn = plt.axes([0.60, 0.15, 0.1, 0.04]) # type: ignore

self.spawn_button = Button(spawn, 'Spawn', hovercolor='0.775')

self.spawn_button.on_clicked(self.spawn_rocket)

launch = plt.axes([0.75, 0.15, 0.1, 0.04]) # type: ignore

self.launch_button = Button(launch, 'Launch', hovercolor='0.775')

self.launch_button.on_clicked(self.launch_rocket)

  
  

def update_dt(self, n):

self.dt = n

  

def reset(self, event):

self.slider.reset()

  

def reset_sim(self, event):

self.dt = 0

self.slider.reset()

self.bodies = copy.deepcopy(self.init_copy)

  

def pause(self, event):

self.dt = 0

  

def play(self, event):

self.dt = self.slider.val

  

def spawn_rocket(self, event):

pass

  

def launch_rocket(self, event):

earth_pos = self.bodies["earth"][2]

earth_vel = self.bodies["earth"][3]

rocket_pos = earth_pos.copy()

rocket_vel = earth_vel.copy()

line, = self.ax.plot([], [], 'w--', linewidth=1)

self.bodies["rocket"] = [Circle((5, -5), 0.5, fc='white', zorder=3),0.01,rocket_pos + np.array([0.0, -3.0]),rocket_vel + np.array([-0.15, 0.0]),Circle((5, -5), 0, alpha=0),line]

self.ax.add_patch(self.bodies["rocket"][0])

def calculate_transfer(self):

e, m, s = self.bodies["earth"][2], self.bodies["mars"][2], self.sun_pos

x1, y1, x2, y2, xs, ys = e[0], e[1], m[0], m[1], s[0], s[1]

angle1 = np.arctan2(y1-ys, x1-xs)

angle2 = np.arctan2(y2-ys, x2-xs)

window = 2*np.pi-(angle2 - angle1) % (2*np.pi)

print()

  

def init(self):

for _, data in self.bodies.items():

self.ax.add_patch(data[4])

self.ax.add_patch(data[0])

self.ax.add_patch(self.sun)

return []

  

def calculate_gravity(self, pos1, pos2, mass):

displacement = pos1 - pos2

r = np.linalg.norm(displacement)

if r < 1e-6:

return np.zeros(2)

else:

unit = displacement / r

gravity_force = self.GRAV_CONSTANT * (mass / (r**2)) * unit

return gravity_force

  

def calculate_orbit(self, pos1, pos2, mass, vec):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = self.GRAV_CONSTANT * mass

a = 1 / (2 / mod_r - mod_v_squared / mew)

e_vec = ((mod_v_squared - mew / mod_r) * displacement - np.dot(displacement, vec) * vec) / mew

e = np.linalg.norm(e_vec)

if e > 0.0005:

omega = np.arctan2(e_vec[1], e_vec[0])

else:

e = 0.0

omega = 0.0

theta = np.linspace(0, 2 * np.pi, 80)

r_orbit = (a * (1 - e**2)) / (1 + e * np.cos(theta))

r_orbit[np.abs(r_orbit) > 1000] = np.nan

x_local = r_orbit * np.cos(theta)

y_local = r_orbit * np.sin(theta)

x_world = pos2[0] + (x_local * np.cos(omega) - y_local * np.sin(omega))

y_world = pos2[1] + (x_local * np.sin(omega) + y_local * np.cos(omega))

  

return x_world, y_world

def in_influence(self, pos1, pos2, radius):

return np.linalg.norm(pos1 - pos2) < radius

def get_influence(self, current_name, current_pos):

for name, data in self.bodies.items():

if name != current_name:

soi_radius = data[4].get_radius()

if self.in_influence(current_pos, data[2], soi_radius):

return name

return "sun"

def animate(self, j):

parents = {}

new_states = {}

# Substeps for more precise calculations

sub_steps = max(1, int(np.round(self.dt / self.step_size)))

small_dt = self.dt / sub_steps

  

for i in range(sub_steps):

for name, data in self.bodies.items():

current_pos = data[2].copy()

current_vel = data[3].copy()

parent = self.get_influence(name, current_pos)

parents[name] = parent

  

if parent == "sun":

current_vel += self.calculate_gravity(self.sun_pos, current_pos, self.sun_mass) * small_dt

else:

parent_data = self.bodies[parent]

current_vel += self.calculate_gravity(self.sun_pos, parent_data[2], self.sun_mass) * small_dt

current_vel += self.calculate_gravity(parent_data[2], current_pos, parent_data[1]) * small_dt

  

current_pos += current_vel * small_dt

new_states[name] = (current_pos, current_vel)

  

for name, (pos, vel) in new_states.items():

self.bodies[name][2] = pos

self.bodies[name][3] = vel

  

self.sun.center = self.sun_pos

  

for name, data in self.bodies.items():

data[0].center = data[2]

data[4].center = data[2]

if parents[name] == "sun":

x_pts, y_pts = self.calculate_orbit(data[2], self.sun_pos, self.sun_mass, data[3])

else:

parent_data = self.bodies[parents[name]]

parent_pos = parent_data[2]

parent_mass = parent_data[1]

parent_vel = parent_data[3]

  

rel_pos = data[2] - parent_pos

rel_vel = data[3] - parent_vel

  

x_local, y_local = self.calculate_orbit(rel_pos, np.array([0.0, 0.0]), parent_mass, rel_vel)

x_pts = x_local + parent_pos[0]

y_pts = y_local + parent_pos[1]

  

data[5].set_data(x_pts, y_pts)

#self.calculate_transfer()

return []

  

def run(self):

self.anim = FuncAnimation(self.fig, self.animate,

init_func=self.init,

frames=360,

interval=20,

blit=False)

try:

plt.show()

except KeyboardInterrupt:

pass

  

if __name__ == "__main__":

sim = OrbitalSimulation()

sim.run()
```

#### Rename for clarity

```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle, Rectangle

from matplotlib.widgets import Button, Slider

from mpl_interactions import ioff, panhandler, zoom_factory

import copy

  
  

class OrbitalSimulation:

def __init__(self):

with plt.ioff():

self.fig = plt.figure()

self.fig.set_dpi(100)

self.fig.set_size_inches(10, 10

)

with plt.ioff():

self.ax = plt.axes([0.1, 0.25, 0.8, 0.70], xlim=(0, 300), ylim=(0, 300)) # type: ignore

self.ax.set_facecolor('black')

  

# Sun won't change

self.sun = Circle((5, -5), 4, fc='orange')

self.sun_mass = 250

self.sun_pos = np.array([150.0, 150.0])

  

# Planet dict: Circle, Mass, Position, Velocity, SOI Circle, Orbit

self.bodies = {

"mercury": {

"body": Circle((5, -5), 0.4, fc='darkgrey', zorder=3),

"mass": 2,

"pos": np.array([150.0, 175.0]),

"vel": np.array([0.316, 0.0]),

"soi": Circle((5, -5), 1.5, fc='grey', alpha=0.15, zorder=2)

},

  

"venus": {

"body": Circle((5, -5), 0.7, fc='gold', zorder=3),

"mass": 6,

"pos": np.array([150.0, 195.0]),

"vel": np.array([0.235, 0.0]),

"soi": Circle((5, -5), 3.5, fc='grey', alpha=0.15, zorder=2)

},

  

"earth": {

"body": Circle((5, -5), 0.75, fc='blue', zorder=3),

"mass": 10,

"pos": np.array([150.0, 220.0]),

"vel": np.array([0.195, 0.0]),

"soi": Circle((5, -5), 6.5, fc='grey', alpha=0.15, zorder=2)

},

  

"moon": {

"body": Circle((5, -5), 0.2, fc='grey', zorder=3),

"mass": 1,

"pos": np.array([150.0, 224.5]),

"vel": np.array([0.345, 0.0]),

"soi": Circle((5, -5), 0.8, fc='grey', alpha=0.05, zorder=2)

},

  

"mars": {

"body": Circle((5, -5), 0.5, fc='red', zorder=3),

"mass": 4,

"pos": np.array([150.0, 25.0]),

"vel": np.array([-0.144, 0.0]),

"soi": Circle((5, -5), 4.0, fc='grey', alpha=0.15, zorder=2)

}

}

  

self.init_copy = copy.deepcopy(self.bodies)

  
  
  
  

self.orbit_lines = []

for _, data in self.bodies.items():

line, = self.ax.plot([], [], 'r--', linewidth=0.9, label="Orbit Path", zorder=1)

  

data["orbit_line"] = line

  
  

self.GRAV_CONSTANT = 0.01

self.dt = 0

self.step_size = 0.1

  
  

self.setup_widgets()

self.disconnect_zoom = zoom_factory(self.ax)

self.pan_handler = panhandler(self.fig, button=1)

  
  
  

def setup_widgets(self):

ax_slider = plt.axes([0.15, 0.08, 0.2, 0.03]) # type: ignore

self.slider = Slider(ax_slider, 'Time', 0, 10, valinit=0.7, valfmt='%1.3f')

self.slider.on_changed(self.update_dt)

  

pause_sim = plt.axes([0.15, 0.15, 0.1, 0.04]) # type: ignore

self.pause_button = Button(pause_sim, 'Pause', hovercolor='0.775')

self.pause_button.on_clicked(self.pause)

  

play_sim = plt.axes([0.25, 0.15, 0.1, 0.04]) # type: ignore

self.button = Button(play_sim, 'Play', hovercolor='0.775')

self.button.on_clicked(self.play)

  

reset_time = plt.axes([0.35, 0.15, 0.1, 0.04]) # type: ignore

self.reset_button = Button(reset_time, 'Reset', hovercolor='0.775')

self.reset_button.on_clicked(self.reset)

  

reset_simulation = plt.axes([0.65, 0.04, 0.15, 0.04]) # type: ignore

self.reset_sim_button = Button(reset_simulation, 'Reset Simulation', hovercolor='0.775')

self.reset_sim_button.on_clicked(self.reset_sim)

  

spawn = plt.axes([0.60, 0.15, 0.1, 0.04]) # type: ignore

self.spawn_button = Button(spawn, 'Spawn', hovercolor='0.775')

self.spawn_button.on_clicked(self.spawn_rocket)

  
  

speed_up = plt.axes([0.75, 0.15, 0.1, 0.04]) # type: ignore

self.speed_up_button = Button(speed_up, 'Speed_up', hovercolor='0.775')

self.speed_up_button.on_clicked(self.speed_up)

slow_down = plt.axes([0.85, 0.15, 0.1, 0.04]) # type: ignore

self.slow_down_button = Button(slow_down, 'Slow_down', hovercolor='0.775')

self.slow_down_button.on_clicked(self.slow_down)

  
  

def update_dt(self, n):

self.dt = n

  

def reset(self, event):

self.slider.reset()

  

def reset_sim(self, event):

self.dt = 0

self.slider.reset()

self.bodies = copy.deepcopy(self.init_copy)

  

def pause(self, event):

self.dt = 0

  

def play(self, event):

self.dt = self.slider.val

  

def spawn_rocket(self, event):

earth_pos = self.bodies["earth"]["pos"]

earth_vel = self.bodies["earth"]["vel"]

rocket_pos = earth_pos.copy()

rocket_vel = earth_vel.copy()

line, = self.ax.plot([], [], 'w--', linewidth=1)

self.bodies["rocket"] = { "body": Circle((5, -5), 0.5, fc='white', zorder=3),

"mass": 0.01,

"pos": rocket_pos + np.array([0.0, -3.0]),

"vel": rocket_vel + np.array([-0.15, 0.0]),

"soi": Circle((5, -5), 0, alpha=0),

"orbit_line": line }

self.ax.add_patch(self.bodies["rocket"]["body"])

  

def speed_up(self, event):

v_norm = np.linalg.norm(self.bodies["rocket"]["vel"])

v_unit = self.bodies["rocket"]["vel"] / v_norm

  

self.bodies["rocket"]["vel"] += v_unit/100

  

def slow_down(self, event):

v_norm = np.linalg.norm(self.bodies["rocket"]["vel"])

v_unit = self.bodies["rocket"]["vel"] / v_norm

  

self.bodies["rocket"]["vel"] -= v_unit/100

  

def calculate_launch(self, target_pos, rocket_pos):

displacement = target_pos - rocket_pos

r = np.linalg.norm(displacement)

  

if r < 1e-6:

return False

r_unit = displacement / r

v_norm = np.linalg.norm(self.bodies["rocket"]["vel"])

if v_norm < 1e-6:

return False

v_unit = self.bodies["rocket"]["vel"] / v_norm

alignment = np.dot(v_unit, r_unit)

return alignment > 0.9995

  
  

def calculate_transfer(self):

if "rocket" not in self.bodies:

return

  

e, m, s = self.bodies["earth"]["pos"], self.bodies["mars"]["pos"], self.sun_pos

x1, y1, x2, y2, xs, ys = e[0], e[1], m[0], m[1], s[0], s[1]

angle1 = np.arctan2(y1-ys, x1-xs)

angle2 = np.arctan2(y2-ys, x2-xs)

window = 2 * np.pi - ( (angle2 - angle1) % (2 * np.pi))

ideal_phase_angle = 0.77

tolerance = 0.05

in_planetary_window = abs(window - ideal_phase_angle) < tolerance

is_aiming_straight = self.calculate_launch(self.bodies["mars"]["pos"], self.bodies["rocket"]["pos"])

print(in_planetary_window, is_aiming_straight)

if in_planetary_window and is_aiming_straight:

self.bodies["rocket"]["vel"] += np.array([0.3, 0.3])

return

  

def init(self):

for _, data in self.bodies.items():

self.ax.add_patch(data["soi"])

self.ax.add_patch(data["body"])

self.ax.add_patch(self.sun)

return []

  

def calculate_gravity(self, pos1, pos2, mass):

displacement = pos1 - pos2

r = np.linalg.norm(displacement)

if r < 1e-6:

return np.zeros(2)

else:

unit = displacement / r

gravity_force = self.GRAV_CONSTANT * (mass / (r**2)) * unit

return gravity_force

  

def calculate_orbit(self, pos1, pos2, mass, vec):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = self.GRAV_CONSTANT * mass

a = 1 / (2 / mod_r - mod_v_squared / mew)

e_vec = ((mod_v_squared - mew / mod_r) * displacement - np.dot(displacement, vec) * vec) / mew

e = np.linalg.norm(e_vec)

if e > 0.0005:

omega = np.arctan2(e_vec[1], e_vec[0])

else:

e = 0.0

omega = 0.0

theta = np.linspace(0, 2 * np.pi, 80)

r_orbit = (a * (1 - e**2)) / (1 + e * np.cos(theta))

r_orbit[np.abs(r_orbit) > 1000] = np.nan

x_local = r_orbit * np.cos(theta)

y_local = r_orbit * np.sin(theta)

x_world = pos2[0] + (x_local * np.cos(omega) - y_local * np.sin(omega))

y_world = pos2[1] + (x_local * np.sin(omega) + y_local * np.cos(omega))

  

return x_world, y_world

def in_influence(self, pos1, pos2, radius):

return np.linalg.norm(pos1 - pos2) < radius

def get_influence(self, current_name, current_pos):

for name, data in self.bodies.items():

if name != current_name:

soi_radius = data["soi"].get_radius()

if self.in_influence(current_pos, data["pos"], soi_radius):

return name

return "sun"

def animate(self, j):

parents = {}

new_states = {}

# Substeps for more precise calculations

sub_steps = max(1, int(np.round(self.dt / self.step_size)))

small_dt = self.dt / sub_steps

  

for i in range(sub_steps):

for name, data in self.bodies.items():

current_pos = data["pos"].copy()

current_vel = data["vel"].copy()

parent = self.get_influence(name, current_pos)

parents[name] = parent

  

if parent == "sun":

current_vel += self.calculate_gravity(self.sun_pos, current_pos, self.sun_mass) * small_dt

else:

parent_data = self.bodies[parent]

current_vel += self.calculate_gravity(self.sun_pos, parent_data["pos"], self.sun_mass) * small_dt

current_vel += self.calculate_gravity(parent_data["pos"], current_pos, parent_data["mass"]) * small_dt

  

current_pos += current_vel * small_dt

new_states[name] = (current_pos, current_vel)

  

for name, (pos, vel) in new_states.items():

self.bodies[name]["pos"] = pos

self.bodies[name]["vel"] = vel

  

self.sun.center = self.sun_pos

  

for name, data in self.bodies.items():

data["body"].center = data["pos"]

data["soi"].center = data["pos"]

if parents[name] == "sun":

x_pts, y_pts = self.calculate_orbit(data["pos"], self.sun_pos, self.sun_mass, data["vel"])

else:

parent_data = self.bodies[parents[name]]

parent_pos = parent_data["pos"]

parent_mass = parent_data["mass"]

parent_vel = parent_data["vel"]

  

rel_pos = data["pos"] - parent_pos

rel_vel = data["vel"] - parent_vel

  

x_local, y_local = self.calculate_orbit(rel_pos, np.array([0.0, 0.0]), parent_mass, rel_vel)

x_pts = x_local + parent_pos[0]

y_pts = y_local + parent_pos[1]

  

data["orbit_line"].set_data(x_pts, y_pts)

self.calculate_transfer()

return []

  

def run(self):

self.anim = FuncAnimation(self.fig, self.animate,

init_func=self.init,

frames=360,

interval=20,

blit=False)

try:

plt.show()

except KeyboardInterrupt:

pass

  

if __name__ == "__main__":

sim = OrbitalSimulation()

sim.run()
```

#### Move to separated step function so lookahead can work

```
from matplotlib import pyplot as plt

import numpy as np

from matplotlib.animation import FuncAnimation

from matplotlib.patches import Circle, Rectangle

from matplotlib.widgets import Button, Slider

from mpl_interactions import ioff, panhandler, zoom_factory

import copy

import threading

  
  

class OrbitalSimulation:

def __init__(self):

with plt.ioff():

self.fig = plt.figure()

self.fig.set_dpi(100)

self.fig.set_size_inches(10, 10

)

with plt.ioff():

self.ax = plt.axes([0.1, 0.25, 0.8, 0.70], xlim=(0, 300), ylim=(0, 300)) # type: ignore

self.ax.set_facecolor('black')

  

# Sun won't change

self.sun = Circle((5, -5), 4, fc='orange')

self.sun_mass = 250

self.sun_pos = np.array([150.0, 150.0])

  

# Planet dict: Circle, Mass, Position, Velocity, SOI Circle, Orbit

self.bodies = {

"mercury": {

"body": Circle((5, -5), 0.4, fc='darkgrey', zorder=3),

"mass": 2,

"pos": np.array([150.0, 175.0]),

"vel": np.array([0.316, 0.0]),

"soi": Circle((5, -5), 1.5, fc='grey', alpha=0.15, zorder=2)

},

  

"venus": {

"body": Circle((5, -5), 0.7, fc='gold', zorder=3),

"mass": 6,

"pos": np.array([150.0, 195.0]),

"vel": np.array([0.235, 0.0]),

"soi": Circle((5, -5), 3.5, fc='grey', alpha=0.15, zorder=2)

},

  

"earth": {

"body": Circle((5, -5), 0.75, fc='blue', zorder=3),

"mass": 10,

"pos": np.array([150.0, 220.0]),

"vel": np.array([0.195, 0.0]),

"soi": Circle((5, -5), 6.5, fc='grey', alpha=0.15, zorder=2)

},

  

"moon": {

"body": Circle((5, -5), 0.2, fc='grey', zorder=3),

"mass": 1,

"pos": np.array([150.0, 224.5]),

"vel": np.array([0.345, 0.0]),

"soi": Circle((5, -5), 0.8, fc='grey', alpha=0.05, zorder=2)

},

  

"mars": {

"body": Circle((5, -5), 0.5, fc='red', zorder=3),

"mass": 4,

"pos": np.array([150.0, 25.0]),

"vel": np.array([-0.144, 0.0]),

"soi": Circle((5, -5), 4.0, fc='grey', alpha=0.15, zorder=2)

}

}

  

self.init_copy = copy.deepcopy(self.bodies)

  
  
  
  

self.orbit_lines = []

for _, data in self.bodies.items():

line, = self.ax.plot([], [], 'r--', linewidth=0.9, label="Orbit Path", zorder=1)

  

data["orbit_line"] = line

  
  

self.GRAV_CONSTANT = 0.01

self.dt = 0

self.step_size = 0.1

  
  

self.setup_widgets()

self.disconnect_zoom = zoom_factory(self.ax)

self.pan_handler = panhandler(self.fig, button=1)

  
  
  

def setup_widgets(self):

ax_slider = plt.axes([0.15, 0.08, 0.2, 0.03]) # type: ignore

self.slider = Slider(ax_slider, 'Time', 0, 10, valinit=0.7, valfmt='%1.3f')

self.slider.on_changed(self.update_dt)

  

pause_sim = plt.axes([0.15, 0.15, 0.1, 0.04]) # type: ignore

self.pause_button = Button(pause_sim, 'Pause', hovercolor='0.775')

self.pause_button.on_clicked(self.pause)

  

play_sim = plt.axes([0.25, 0.15, 0.1, 0.04]) # type: ignore

self.button = Button(play_sim, 'Play', hovercolor='0.775')

self.button.on_clicked(self.play)

  

reset_time = plt.axes([0.35, 0.15, 0.1, 0.04]) # type: ignore

self.reset_button = Button(reset_time, 'Reset', hovercolor='0.775')

self.reset_button.on_clicked(self.reset)

  

reset_simulation = plt.axes([0.65, 0.04, 0.15, 0.04]) # type: ignore

self.reset_sim_button = Button(reset_simulation, 'Reset Simulation', hovercolor='0.775')

self.reset_sim_button.on_clicked(self.reset_sim)

  

spawn = plt.axes([0.60, 0.15, 0.1, 0.04]) # type: ignore

self.spawn_button = Button(spawn, 'Spawn', hovercolor='0.775')

self.spawn_button.on_clicked(self.spawn_rocket)

  
  

speed_up = plt.axes([0.75, 0.15, 0.1, 0.04]) # type: ignore

self.speed_up_button = Button(speed_up, 'Speed Up', hovercolor='0.775')

self.speed_up_button.on_clicked(self.speed_up)

slow_down = plt.axes([0.85, 0.15, 0.1, 0.04]) # type: ignore

self.slow_down_button = Button(slow_down, 'Slow Down', hovercolor='0.775')

self.slow_down_button.on_clicked(self.slow_down)

  

check_collision = plt.axes([0.95, 0.15, 0.1, 0.04]) # type: ignore

self.check_collision_button = Button(check_collision, 'Check Collision', hovercolor='0.775')

self.check_collision_button.on_clicked(self.calculate_collision)

  
  

def update_dt(self, n):

self.dt = n

  

def reset(self, event):

self.slider.reset()

  

def reset_sim(self, event):

self.dt = 0

self.slider.reset()

self.bodies = copy.deepcopy(self.init_copy)

  

def pause(self, event):

self.dt = 0

  

def play(self, event):

self.dt = self.slider.val

  

def spawn_rocket(self, event):

earth_pos = self.bodies["earth"]["pos"]

earth_vel = self.bodies["earth"]["vel"]

rocket_pos = earth_pos.copy()

rocket_vel = earth_vel.copy()

line, = self.ax.plot([], [], 'w--', linewidth=1)

self.bodies["rocket"] = { "body": Circle((5, -5), 0.5, fc='white', zorder=3),

"mass": 0.01,

"pos": rocket_pos + np.array([0.0, -3.0]),

"vel": rocket_vel + np.array([-0.15, 0.0]),

"soi": Circle((5, -5), 0, alpha=0),

"orbit_line": line }

self.ax.add_patch(self.bodies["rocket"]["body"])

  

def speed_up(self, event):

if "rocket" not in self.bodies:

print("No rocket spawned.")

return

v_norm = np.linalg.norm(self.bodies["rocket"]["vel"])

v_unit = self.bodies["rocket"]["vel"] / v_norm

  

self.bodies["rocket"]["vel"] += v_unit/100

  

def slow_down(self, event):

if "rocket" not in self.bodies:

print("No rocket spawned.")

return

v_norm = np.linalg.norm(self.bodies["rocket"]["vel"])

v_unit = self.bodies["rocket"]["vel"] / v_norm

  

self.bodies["rocket"]["vel"] -= v_unit/100

  

def calculate_launch(self, target_pos, rocket_pos):

displacement = target_pos - rocket_pos

r = np.linalg.norm(displacement)

  

if r < 1e-6:

return False

r_unit = displacement / r

v_norm = np.linalg.norm(self.bodies["rocket"]["vel"])

if v_norm < 1e-6:

return False

v_unit = self.bodies["rocket"]["vel"] / v_norm

alignment = np.dot(v_unit, r_unit)

return alignment > 0.9995

  
  

def calculate_transfer(self):

if "rocket" not in self.bodies:

return

  

e, m, s = self.bodies["earth"]["pos"], self.bodies["mars"]["pos"], self.sun_pos

x1, y1, x2, y2, xs, ys = e[0], e[1], m[0], m[1], s[0], s[1]

angle1 = np.arctan2(y1-ys, x1-xs)

angle2 = np.arctan2(y2-ys, x2-xs)

window = 2 * np.pi - ( (angle2 - angle1) % (2 * np.pi))

ideal_phase_angle = 0.77

tolerance = 0.05

in_planetary_window = abs(window - ideal_phase_angle) < tolerance

is_aiming_straight = self.calculate_launch(self.bodies["mars"]["pos"], self.bodies["rocket"]["pos"])

if in_planetary_window and is_aiming_straight:

self.bodies["rocket"]["vel"] += np.array([0.3, 0.3])

return

def calculate_collision(self, event):

if "rocket" not in self.bodies:

print("No rocket spawned.")

return

thread = threading.Thread(target=self._collision_lookahead, daemon=True)

thread.start()

  
  

def _collision_lookahead(self):

future_bodies = copy.deepcopy(self.bodies)

moon_soi_radius = future_bodies["moon"]["soi"].get_radius()

dt = 1.0

  

for i in range(10000):

self.step(future_bodies, dt)

  

rocket_pos = future_bodies["rocket"]["pos"]

moon_pos = future_bodies["moon"]["pos"]

  

if np.linalg.norm(rocket_pos - moon_pos) < moon_soi_radius:

print("collision")

return

  

print("No collision in lookahead window.")

  

  

def init(self):

for _, data in self.bodies.items():

self.ax.add_patch(data["soi"])

self.ax.add_patch(data["body"])

self.ax.add_patch(self.sun)

return []

  

def calculate_gravity(self, pos1, pos2, mass):

displacement = pos1 - pos2

r = np.linalg.norm(displacement)

if r < 1e-6:

return np.zeros(2)

else:

unit = displacement / r

gravity_force = self.GRAV_CONSTANT * (mass / (r**2)) * unit

return gravity_force

  

def calculate_orbit(self, pos1, pos2, mass, vec):

displacement = pos1 - pos2

mod_r = np.linalg.norm(displacement)

mod_v_squared = np.square(np.linalg.norm(vec))

mew = self.GRAV_CONSTANT * mass

a = 1 / (2 / mod_r - mod_v_squared / mew)

e_vec = ((mod_v_squared - mew / mod_r) * displacement - np.dot(displacement, vec) * vec) / mew

e = np.linalg.norm(e_vec)

if e > 0.0005:

omega = np.arctan2(e_vec[1], e_vec[0])

else:

e = 0.0

omega = 0.0

theta = np.linspace(0, 2 * np.pi, 80)

r_orbit = (a * (1 - e**2)) / (1 + e * np.cos(theta))

r_orbit[np.abs(r_orbit) > 1000] = np.nan

x_local = r_orbit * np.cos(theta)

y_local = r_orbit * np.sin(theta)

x_world = pos2[0] + (x_local * np.cos(omega) - y_local * np.sin(omega))

y_world = pos2[1] + (x_local * np.sin(omega) + y_local * np.cos(omega))

  

return x_world, y_world

def in_influence(self, pos1, pos2, radius):

return np.linalg.norm(pos1 - pos2) < radius

def get_influence(self, current_name, current_pos, bodies=None):

# pass the body of the specified simulation (live or ahead)

if bodies is None:

bodies = self.bodies

for name, data in bodies.items():

if name != current_name:

soi_radius = data["soi"].get_radius()

if self.in_influence(current_pos, data["pos"], soi_radius):

return name

return "sun"

def step(self, bodies, dt):

new_states = {}

for name, data in bodies.items():

current_pos = data["pos"].copy()

current_vel = data["vel"].copy()

parent = self.get_influence(name, current_pos, bodies)

  

if parent == "sun":

current_vel += self.calculate_gravity(self.sun_pos, current_pos, self.sun_mass) * dt

else:

parent_data = bodies[parent]

current_vel += self.calculate_gravity(self.sun_pos, parent_data["pos"], self.sun_mass) * dt

current_vel += self.calculate_gravity(parent_data["pos"], current_pos, parent_data["mass"]) * dt

  

current_pos += current_vel * dt

new_states[name] = (current_pos, current_vel)

  

for name, (pos, vel) in new_states.items():

bodies[name]["pos"] = pos

bodies[name]["vel"] = vel

  

def animate(self, j):

# Substeps for more precise calculations

sub_steps = max(1, int(np.round(self.dt / self.step_size)))

small_dt = self.dt / sub_steps

  

for i in range(sub_steps):

self.step(self.bodies, small_dt)

self.sun.center = self.sun_pos

  

for name, data in self.bodies.items():

data["body"].center = data["pos"]

data["soi"].center = data["pos"]

parent = self.get_influence(name, data["pos"])

if parent == "sun":

x_pts, y_pts = self.calculate_orbit(data["pos"], self.sun_pos, self.sun_mass, data["vel"])

else:

parent_data = self.bodies[parent]

parent_pos = parent_data["pos"]

parent_mass = parent_data["mass"]

parent_vel = parent_data["vel"]

  

rel_pos = data["pos"] - parent_pos

rel_vel = data["vel"] - parent_vel

  

x_local, y_local = self.calculate_orbit(rel_pos, np.array([0.0, 0.0]), parent_mass, rel_vel)

x_pts = x_local + parent_pos[0]

y_pts = y_local + parent_pos[1]

  

data["orbit_line"].set_data(x_pts, y_pts)

self.calculate_transfer()

return []

  

def run(self):

self.anim = FuncAnimation(self.fig, self.animate,

init_func=self.init,

frames=360,

interval=20,

blit=False)

try:

plt.show()

except KeyboardInterrupt:

pass

  

if __name__ == "__main__":

sim = OrbitalSimulation()

sim.run()
```