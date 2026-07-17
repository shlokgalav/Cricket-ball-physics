## Simple bounce model
## Goal
Similar to version 1A, this model relies on basic Newtonian mechanics and projectile motion principles that account only for gravity. However, in this model, I will introduce a new physical element: bounce. In this model, I will incorporate the changes to the ball's trajectory and speed as it makes contact with the pitch. For this model, I will not take into account spin or swing since this serves as a baseline bounce model for the following models.

## Assumptions
- No air resistance
- No spin
- No swing
- No wind
- Simple bounce only
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

$$
v_{x,new} = v_x

Once the ball bounces, the vertical velocity reverses direction and decreases in magnitude by a fixed restitution coefficient, which measures how "bouncy" the collision with a surface is:  

$$
v_{y,bounce} = -e*v_y

Here, e defines how much speed the ball has after the bounce. If e = 1, the bounce is perfectly elastic. elastic. If e = 0, the ball does not bounce. For this model, e I will use 0.6 as the coefficient of restitution. This means that the ball keeps 60% of its vertical speed and reverses direction. 0.6 is chosen as a baseline, not as a universal constant. A specific cricket-ball trajectory simulation study in the Sage Journals by Naveen Kumar specifically compares 0.4 and 0.6, making 0.6 a good baseline value to use for this model.

When the ball reaches the pitch, the model will apply the bounce condition:

$$
y \leq 0
$$

The vertical velocity will reverse direction and decrease in magnitude.


# Expected Model Output
This model should show a basic parabolic trajectory, before the bounce, of the ball as seen in most basic projectile motion problems. After bouncing, the ball's velocity should reduce by a certain factor known as the coefficient of restitution. After the contact with the pitch, the trajectory will be a second, lower parabolic path since the vertical speed of the ball reduces.  

## Model Output
