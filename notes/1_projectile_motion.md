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
$$

The simulation stops when:

$$
y \leq 0
$$

This represents the ball reaching the ground or pitch surface.


# Expected Model Output
This model should show a basic parabolic trajectory of the ball as seen in most basic projectile motion problems. Later on, this model will be compared with the following models, which will include realistic effects to see how factors such as drag, swing, and spin affect the ball's trajectory.

## Model Output
![Basic projectile motion trajectory](../Figures/basic_projectile_motion.png)
