## Simple bounce model
## Goal
Similar to version 1A, this model relies on basic Newtonian mechanics and projectile motion principles, which take into account only gravity. However, in this model, I will introduce a new physical element: bounce. In this model, I will incorporate the changes to the ball's trajectory and speed as it makes contact with the pitch. For this model, I will not take into account spin or swing since this serves as a baseline bounce model for the following models.

## Assumptions
- No air resistance
- No spin
- No swing
- No wind
- No bounce
- Ball is treated as a point mass
- Gravity is constant

  ## Variables
| Variable | Meaning |
|---|---|
| x | horizontal position |
| y | vertical position |
| v0 | initial speed |
| theta | release angle |
| vx | horizontal velocity |
| vy | vertical velocity |
| g | acceleration due to gravity |
| t | time |

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

The position is updated step by step:

$$
x_{new} = x + v_x \Delta t
$$

$$
y_{new} = y + v_y \Delta t
$$

The vertical velocity changes because of gravity:

$$
v_{y,new} = v_y - g\Delta t
$$

The horizontal velocity stays constant in this first model because there is no air resistance:

Once the ball bounces, the vertical velocity reverses direction and decreases in magnitude by a fixed restitution coefficient which measures how "bouncy" the collision with a surface is:  

$$
v_{y,bounce} = -e*v_y

This simulation will not stop when:

$$
y \leq 0
$$

Since I need to incorporate bounce into this model.


# Expected Model Output
This model should show a basic parabolic trajectory of the ball as seen in most basic projectile motion problems. After bouncing, the ball's velocity should reduce by a certain factor known as the coefficient of restitution. After the contact with the pitch, the trajectory will either 

## Model Output
