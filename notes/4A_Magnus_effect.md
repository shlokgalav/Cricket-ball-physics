## Projectile motion with the Magnus effect

## Goal
The goal of the fourth and final model is to create a model for spin bowling. Unlike model 3, model 4 will focus on the Magnus effect, which is more relevant to spin bowling. This model ignores seam-induced swing for model simplicity. The ball's motion will be affected by gravity, drag, and the Magnus effect. Model 4A considers only the ball's motion through the air. Bounce and pitch friction are not included.

## Coordinate System
The model uses three spatial dimensions:

- \(x\): forward distance toward the batter
- \(y\): vertical height above the pitch
- \(z\): sideways displacement

## Assumptions
- The ball is treated as a point mass.
- Gravity is constant.
- The ball has a prescribed angular velocity vector.
- Air resistance is included.
- The drag coefficient is treated as constant.
- The Magnus effect is ignored.
- The Magnus coefficient is treated as constant during a simulation.
- Seam-induced swing is not included.
- Wind is ignored.
- Bounce is ignored in Model 4A.
- Pitch friction is ignored because Model 4A ends when the ball reaches the pitch.
  

  ## New variables: Magnus force and angular velocity
  The cricket ball now has an angular velocity vector:

$$
\vec\omega=
(\omega_x,\omega_y,\omega_z)
$$

The magnitude of the spin rate is:

$$
\omega=
\sqrt{\omega_x^2+\omega_y^2+\omega_z^2}
$$

The direction of \vec\omega represents the spin axis.

Different spin-axis orientations can therefore produce different Magnus-force directions.

The ball will now be affected by the Magnus force:

spinning ball moving through air experiences an aerodynamic force associated with the Magnus effect.

The Magnus force is modeled as:

$$
\boxed{
\vec F_M=
\frac12\rho A C_Mv^2
\frac{\vec\omega\times\vec v}
{\left|\vec\omega\times\vec v\right|}
}
$$

The magnitude is:

$$
F_M=
\frac12\rho A C_Mv^2
$$

while the direction is determined by:

$$
\vec\omega\times\vec v
$$

The cross product produces a direction perpendicular to both the spin axis and the velocity vector.

This Magnus force equation is taken from Chinagodaba et al. (2026), who used it in a six-degree-of-freedom cricket spin-bowling flight model.


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
| Cm | Magnus coefficient |
| F_magnus | Magnus force |
| \vec\omega | angular velocity |
| rho | air density |
| Cd | drag coefficient |
| F_drag | magnitude of drag force |
| ax | horizontal acceleration |
| ay | vertical acceleration |
| az | sideways acceleration |
| dt | time step |

