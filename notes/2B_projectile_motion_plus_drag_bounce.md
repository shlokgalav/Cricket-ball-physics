# Projectile motion with drag and bounce

## Goal
The second version of this model will take into account Newtonian mechanics and projectile motion principles that account for gravity along with air resistance. This is the next level, which will be compared to the baseline models from version 1B. Model 2B will also account for bounce along with the other principles. Similar to model 1, the ball will still be treated like a point mass.

## Assumptions
- The ball is treated as a point mass.
- Gravity is constant.
- Air resistance is included.
- Drag acts opposite the ball’s velocity.
- The drag coefficient is treated as constant.
- Wind is ignored.
- Spin is ignored.
- Swing is ignored.
-  One simple bounce is included.
- The coefficient of restitution is constant and set to \(e = 0.6\).
- The pitch is treated as a flat surface at \(y = 0\).
- Only vertical velocity changes instantaneously during the bounce.
- Horizontal friction during contact with the pitch is ignored.
- The simulation stops when the ball reaches the pitch for the second time.

    ## Variables
| Variable | Meaning |
|---|---|
| x | horizontal position |
| y | vertical position |
| vx | horizontal velocity |
| vy | vertical velocity |
| v | total speed |
| g | acceleration due to gravity |
| m | mass of cricket ball |
| r | radius of cricket ball |
| A | cross-sectional area of cricket ball |
| rho | air density |
| Cd | drag coefficient |
| F_drag | magnitude of drag force |
| ax | horizontal acceleration |
| ay | vertical acceleration |
| dt | time step |
| e | coefficient of restitution |


## Basic Equations

The initial velocity is split into horizontal and vertical components:

$$
v_x = v_0 \cos(\theta)
$$

$$
v_y = v_0 \sin(\theta)
$$

The speed of the ball can be written as:

$$
v = \sqrt{v_x^2 + v_y^2}
$$

The drag force magnitude:

$$
F_{\text{drag}} = \frac{1}{2}\rho C_d A v^2
$$

Components of drag force:

$$
F_{\text{drag},x} = -F_{\text{drag}} \frac{v_x}{v}
$$

$$
F_{\text{drag},y} = -F_{\text{drag}} \frac{v_y}{v}
$$

The x and y components of the drag force come from the idea of a unit vector:

$$
\hat{v}_x = \frac{v_x}{v}
$$

$$
\hat{v}_y = \frac{v_y}{v}
$$

Therefore, the drag force vector is:

$$
\vec{F}_D = -F_D \frac{\vec{v}}{v}
$$

So the drag force components are:

$$
F_{D,x} = -F_D \frac{v_x}{v}
$$

$$
F_{D,y} = -F_D \frac{v_y}{v}
$$

Negative sign signifies that the drag force acts opposite the velocity

Acceleration calculation using Newton's second law:

$$
F = ma
$$

$$
ax = F_drag_x / m
$$

$$
ay = -g + F_drag_y / m
$$

Updating velocity:

$$
vx_new = vx + ax * dt
$$

$$
vy_new = vy + ay * dt
$$

Updating position:

$$
x_new = x + vx * dt
$$

$$
y_new = y + vy * dt
$$

Once the ball bounces, the vertical velocity reverses direction and decreases in magnitude by a fixed restitution coefficient, which measures how "bouncy" the collision with a surface is:  

$$
v_{y,bounce} = -e*v_y
$$

When the ball reaches the pitch, the model will apply the bounce condition:

$$
y \leq 0
$$

The vertical velocity will reverse direction and decrease in magnitude.


## Expected Model Output
When compared to model 1, this model should show the ball travelling a smaller horizontal distance since air resistance is acting opposite the velocity. The trajectory will still curve downward, but the ball will reach the pitch at a smaller horizontal distance. After the contact with the pitch, the trajectory after the bounce will be similar, with the only difference being a smaller vertical velocity due to air resistance. 

## Model 2B Output

This second model considers drag and gravity along with a simple bounce.

![Projectile motion with drag and bounce](figures/projectile_motion_with_drag_bounce.png)





