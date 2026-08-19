# Projectile motion with aerodynamic effects 

## Goal
The goal of the third model is to include more realistic physical effects. This model will consider gravity and air resistance just like the previous models. This model expands on model 2A by introducing aerodynamic drag and seam-induced swing. Unlike other models, we will now also consider motion in three dimensions to model sideways motion due to aerodynamic drag. Model 3A will not include bounce as it will only consider the motion of the ball in the air.

## Coordinate System
The model uses three spatial dimensions:

- \(x\): forward distance toward the batter
- \(y\): vertical height above the pitch
- \(z\): sideways displacement

## Assumptions
- The ball is treated as a point mass.
- Gravity is constant.
- Air resistance is included.
- The drag coefficient is treated as constant.
- Seam-induced swing is represented using a simplified aerodynamic swing coefficient.
- The aerodynamic coefficients are treated as constant during a single simulation.
- Wind is ignored.
- Bounce is ignored in Model 3A.

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
| Cs | swing-force coefficient |
| F_swing | seam-induced swing-force magnitude |
| rho | air density |
| Cd | drag coefficient |
| F_drag | magnitude of drag force |
| ax | horizontal acceleration |
| ay | vertical acceleration |
| az | sideways acceleration |
| dt | time step |

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

(Initial sideways velocity is zero as the bowler bowls)

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

This equation follows from the force-coefficient formulation used for cricket-ball swing by Grimshaw, Briggs, and Atkins (2024) in a research paper.


The coefficient (C_S) represents the aerodynamic asymmetry produced by factors such as seam orientation and ball-surface condition.


In this simplified model, swing is assumed to act in the sideways (z)-direction.


For this model, a C_S value of 0.30 will be used, as in the research paper by Grimshaw, Briggs, and Atkins (2024), they measured the coefficient in the range of 0.25 to 0.35.


A signed value of (C_S) can represent the direction of swing:

(C_S>0): swing in the positive (z)-direction
(C_S<0): swing in the negative (z)-direction
(C_S=0): no seam-induced swing

Therefore:

$$
F_{S,z}=F_S
$$

while the simplified model assumes:

$$
F_{S,x}=0
$$

$$
F_{S,y}=0
$$


This force is purely sideways.


The aerodynamic drag force then becomes the net force of the swing force and drag force:

$$
\vec F_aero = \vec F_D + \vec F_S
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


## Expected Model Output

Model 3A should be compared to Model 2A. In comparison, Model 3A will have sideways motion. The vertical and horizontal trajectories will remain the same since we still have the drag force and gravity acting on the ball. The sideways velocity should start at zero and then increase as a result of the swing force. The main new result should be a three-dimensional trajectory showing seam-induced swing during flight.








