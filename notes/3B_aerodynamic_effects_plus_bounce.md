## Projectile motion with aerodynamic effects and bounce

## Goal
The goal of the third model is to include more realistic physical effects. This model will consider gravity and air resistance just like the previous models. This model expands on model 2B by introducing seam-induced swing. Unlike other models, we will now also consider three-dimensional motion to account for sideways motion due to aerodynamic drag. Model 3B will include bounce by considering the ball's motion in the air before and after the bounce, incorporating new aerodynamic effects.

## Assumptions
- The ball is treated as a point mass.
- Gravity is constant.
- Air resistance is included.
- The drag coefficient is treated as constant.
- Seam-induced swing is represented using a simplified aerodynamic swing coefficient.
- The aerodynamic coefficients are treated as constant during a single simulation.
- Wind is ignored.
- A simple bounce is included.
- The coefficient of restitution is constant and set to \(e = 0.6\).
- The pitch is treated as a flat surface at \(y = 0\).
- Only vertical velocity changes instantaneously during the bounce.
- Horizontal friction during contact with the pitch is ignored.
- Sideways friction during contact with the pitch is ignored.
- The simulation stops when the ball reaches the pitch for the second time.
- The Magnus effect is ignored.
- Spin-related aerodynamic effects are reserved for Model 4.

     ## Variables
| Variable | Meaning |
|---|---|
| x | horizontal position |
| y | vertical position |
| z | sideways position |
| vx | horizontal velocity |
| vy | vertical velocity |
| vz | sideways velocity |
| v | total speed |
| g | acceleration due to gravity |
| m | mass of cricket ball |
| r | radius of cricket ball |
| A | cross-sectional area of cricket ball |
| Cs | swing-force coefficient |
| F_swing | seam-induced swing-force magnitude |
| rho | air density |
| Cd | drag coefficient |
| F_drag | magnitude of drag force |
| ax | horizontal acceleration |
| ay | vertical acceleration |
| az | sideways acceleration |
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

$$
v_z = 0  
$$


The speed of the ball can be written as:

$$
v = \sqrt{v_x^2 + v_y^2 + v_z^2}
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

Gravity acts only in the vertical direction:

$$
F_{g,y}=-mg
$$

Therefore:

$$
a_{g,y}=-g
$$

The swing force magnitude:

$$
F_S=\frac{1}{2}\rho C_S A v^2
$$


$$
F_{S,z}=F_S
$$

The simplified model assumes:

$$
F_{S,x}=0
$$

$$
F_{S,y}=0
$$


Net force and acceleration:

$$
\vec F_net = \vec F_g + \vec F_D + \vec F_S
$$


Net acceleration:


Horizontal:

$$
\vec a_x = \frac{F_{D,x}}{m}
$$

Vertical:

$$
a_y=-g+\frac{F_{D,y}}{m}
$$

Sideways:

$$
a_z=\frac{F_{D,z}+F_{S,z}}{m}
$$

Updating position:

$$
x_{\text{new}}=x+v_x\Delta t
$$

$$
y_{\text{new}}=y+v_y\Delta t
$$

$$
z_{\text{new}}=z+v_z\Delta t
$$

Updating velocity:

$$
v_{x,\text{new}}=v_x+a_x\Delta t
$$

$$
v_{y,\text{new}}=v_y+a_y\Delta t
$$

$$
v_{z,\text{new}}=v_z+a_z\Delta t
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


Because detailed pitch friction is not modeled:

$$
v_{x,\text{before}} = v_{x,\text{before}}
$$

and:

$$
v_{z,\text{before}} = v_{z,\text{before}}
$$

This is a simplifying assumption.

Detailed changes in sideways motion, spin, friction, and turn during pitch contact will be reserved for Model 4.


## Expected Model Output
Model 3B will be compared to Model 2B. The forward and vertical motion should remain broadly similar to Model 2B, as the drag force and gravity are still present. The ball should develop some sideways motion before the bounce. The sideways velocity and forward velocity should not change due to the bounce since pitch friction is ignored. The primary output should be a three-dimensional trajectory showing seam-induced swing before and after one simplified bounce.

## Model 3B Output

This third model considers gravity, drag, seam-induced swing, and bounce.

![projectile motion with swing](../figures/projectile_motion_with_swing_bounce.png)



