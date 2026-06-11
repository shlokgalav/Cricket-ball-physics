# Projectile Motion

## Goal
The first version of the model relies on basic Newtonian mechanics and projectile motion principles, which take into account only gravity. This is the baseline model, which helps in understanding the simplest possible motion of the ball before understanding how factors such as drag, swing, spin, or surface interaction affect the motion of a cricket ball. For this model, the ball will be treated as a point mass, and the bounce will not be included in this model since it will add a second layer of physics.

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
Initial velocity components:
vx = v0 cos(theta)
vy = v0 sin(theta)
vi = $\{vx + vy}$

Position:
x_new = x + vx * dt
y_new = y + vy * dt

Velocity update:
vy_new = vy - g * dt
vx is constant throughout since there is no force in the X - direction.

# Predicted model output
This model should show a basic parabolic trajectory of the ball as seen in most basic projectile motion problems. Later on, this model will be compared with the following models, which will include realistic effects to see how factors such as drag, swing, and spin affect the ball's trajectory.
