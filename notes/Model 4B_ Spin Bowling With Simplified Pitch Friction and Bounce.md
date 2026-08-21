# Model 4B: Spin Bowling With Simplified Pitch Friction and Bounce

## Goal

Model 4B extends Model 4A by adding a simplified interaction between the spinning cricket ball and the pitch.

During flight, the ball is affected by:

- gravity
- aerodynamic drag
- the Magnus effect

When the ball first reaches the pitch, the model includes:

- a vertical bounce
- friction between the cricket ball and pitch
- a simplified sideways change in velocity representing turn off the pitch

The purpose of Model 4B is to model the two main stages of a spin-bowling delivery:

1. aerodynamic movement caused by spin while the ball is in the air
2. sideways deviation caused by friction when the spinning ball contacts the pitch

The model deliberately simplifies the ball-pitch collision so that detailed rotational contact mechanics are not required.

---

## Coordinate System

The same coordinate system from Models 3 and 4A is used:

- \(x\): forward distance toward the batter
- \(y\): vertical height above the pitch
- \(z\): sideways displacement

The ball's linear velocity is:

$$
\vec v=(v_x,v_y,v_z)
$$

The angular velocity of the spinning ball is:

$$
\vec\omega=(\omega_x,\omega_y,\omega_z)
$$

---

## Assumptions

- The translational motion of the ball is tracked through its center of mass.
- Gravity is constant.
- Air resistance is included.
- The drag coefficient is treated as constant.
- The Magnus effect is included during flight.
- The Magnus coefficient is treated as constant.
- The angular velocity vector is treated as constant during flight.
- Wind is ignored.
- Seam-induced swing is not included separately.
- One bounce is included.
- The pitch is represented as a flat surface at \(y=0\).
- The coefficient of restitution is treated as constant.
- The coefficient of friction between the ball and pitch is treated as constant.
- The collision with the pitch is treated as instantaneous.
- The ball is assumed to slide during the simplified pitch contact.
- Pitch friction is modeled only through a sideways frictional impulse that produces turn.
- The forward velocity is not changed instantaneously by pitch friction in this simplified model.
- Detailed torque and angular-momentum transfer between the ball and pitch are not modeled.
- The ball's spin vector is not changed during the bounce.
- The simulation stops when the ball reaches the pitch for the second time.

---

## Variables

| Variable | Meaning |
|---|---|
| \(x\) | forward position |
| \(y\) | vertical position |
| \(z\) | sideways position |
| \(v_x\) | forward velocity |
| \(v_y\) | vertical velocity |
| \(v_z\) | sideways velocity |
| \(v\) | total speed |
| \(m\) | mass of cricket ball |
| \(r\) | radius of cricket ball |
| \(A\) | cross-sectional area |
| \(\rho\) | air density |
| \(C_D\) | drag coefficient |
| \(C_M\) | Magnus coefficient |
| \(\vec\omega\) | angular velocity vector |
| \(F_D\) | drag-force magnitude |
| \(\vec F_M\) | Magnus-force vector |
| \(g\) | gravitational acceleration |
| \(e\) | coefficient of restitution |
| \(\mu\) | coefficient of friction |
| \(J_n\) | normal impulse during the bounce |
| \(J_f\) | sideways frictional impulse |
| \(s\) | direction of friction-induced turn |
| \(dt\) | simulation time step |

---

## Flight Before the Bounce

Before the ball reaches the pitch, Model 4B uses the same flight equations as Model 4A.

### Total Speed

$$
v=
\sqrt{v_x^2+v_y^2+v_z^2}
$$

---

## Gravity

Gravity acts vertically downward:

$$
\vec F_g=(0,-mg,0)
$$

---

## Aerodynamic Drag

The drag-force magnitude is:

$$
F_D=
\frac{1}{2}\rho C_DAv^2
$$

Drag acts opposite the direction of motion:

$$
\vec F_D=
-F_D\frac{\vec v}{v}
$$

---

## Magnus Effect

The Magnus force caused by the spinning ball is:

$$
\boxed{
\vec F_M=
\frac{1}{2}\rho AC_Mv^2
\frac{\vec\omega\times\vec v}
{\left|\vec\omega\times\vec v\right|}
}
$$

The cross product determines the direction of the Magnus force.

This formulation is taken from Chinagodaba et al. (2026), who used gravity, drag, and a Magnus-type force to model cricket spin-bowling trajectories.

For the baseline simulation:

$$
C_M=0.18
$$

as established in Model 4A.

---

## Net Force During Flight

Before and after the bounce, while the ball is airborne:

$$
\boxed{
\vec F_{\text{net}}
=
\vec F_g+\vec F_D+\vec F_M
}
$$

Newton's second law gives:

$$
\vec a=
\frac{\vec F_{\text{net}}}{m}
$$

The position and velocity are then updated using the same numerical method as the previous models.

---

# Pitch Interaction

## First Pitch Contact

The first pitch contact occurs when:

$$
y\leq0
$$

The vertical position is reset to:

$$
y=0
$$

Two simplified effects are then applied:

1. vertical bounce
2. sideways frictional impulse

---

## Vertical Bounce

As in the previous bounce models, the vertical velocity reverses direction and decreases in magnitude:

$$
\boxed{
v_{y,\text{after}}
=
-e\,v_{y,\text{before}}
}
$$

For consistency with Models 1B, 2B, and 3B:

$$
e=0.60
$$

The value \(e=0.60\) is retained as a project modeling assumption rather than introduced as a new literature-derived constant.

---

# Normal Impulse

Impulse represents the change in momentum during the short collision.

The normal impulse from the pitch is:

$$
J_n
=
m
\left(
v_{y,\text{after}}
-
v_{y,\text{before}}
\right)
$$

Using the restitution equation:

$$
v_{y,\text{after}}
=
-e\,v_{y,\text{before}}
$$

gives:

$$
J_n
=
-m(1+e)v_{y,\text{before}}
$$

Because the ball is moving downward immediately before impact:

$$
v_{y,\text{before}}<0
$$

the magnitude of the normal impulse can be written as:

$$
\boxed{
J_n=
m(1+e)
\left|v_{y,\text{before}}\right|
}
$$

This follows directly from the impulse-momentum and coefficient-of-restitution relationships used in collision mechanics.

---

# Pitch Friction

A spinning cricket ball can interact with the pitch through friction.

Cricket ball-pitch simulations by Pandey and Rao (2020) found that changing the coefficient of friction affects rebound angle, rebound velocity, and post-impact spin.

For the simplified baseline:

$$
\boxed{\mu=0.30}
$$

Pandey and Rao used \(\mu=0.30\) in one of their cricket ball-pitch simulations and also investigated a wider range of friction coefficients.

---

## Frictional Impulse

Instead of calculating the friction force during every instant of the very short collision, Model 4B represents friction using an impulse.

For a sliding collision, a simplified Coulomb-friction impulse can be written as:

$$
\boxed{
J_f=\mu J_n
}
$$

This sliding-regime relationship is used in impulse-based collision models, including Doménech-Carbó (2024).

Substituting the normal impulse gives:

$$
J_f=
\mu m(1+e)
\left|v_{y,\text{before}}\right|
$$

---

# Sideways Change in Velocity

Impulse is related to change in momentum:

$$
J_f=m\Delta v_z
$$

Therefore:

$$
\Delta v_z=
\frac{J_f}{m}
$$

Substituting the frictional impulse gives:

$$
\boxed{
\Delta v_z=
\mu(1+e)
\left|v_{y,\text{before}}\right|
}
$$

This equation is a simplified result obtained by combining:

1. the normal restitution relationship
2. impulse-momentum
3. the sliding-friction impulse relation \(J_f=\mu J_n\)

---

## Direction of Turn

Friction must also have a direction.

The simplified model introduces:

$$
s=\pm1
$$

where:

- \(s=+1\): friction produces turn in the positive \(z\)-direction
- \(s=-1\): friction produces turn in the negative \(z\)-direction

The value of \(s\) is chosen according to the direction of the ball's spin.

The sideways velocity immediately after the bounce becomes:

$$
\boxed{
v_{z,\text{after}}
=
v_{z,\text{before}}
+
s\mu(1+e)
\left|v_{y,\text{before}}\right|
}
$$

This is the main new equation introduced in the simplified Model 4B.

It represents the idea that spin causes the ball to slip against the pitch, friction acts during that contact, and the resulting impulse produces sideways deviation.

---

## Forward Velocity During the Bounce

In the simplified model, pitch friction is used only to represent sideways turn.

Therefore:

$$
\boxed{
v_{x,\text{after}}
=
v_{x,\text{before}}
}
$$

In reality, friction and deformation during pitch contact can also change the forward speed of the ball.

That effect is deliberately ignored to keep Model 4B focused on sideways turn.

---

## Spin During the Bounce

The angular velocity is also kept constant:

$$
\boxed{
\vec\omega_{\text{after}}
=
\vec\omega_{\text{before}}
}
$$

This is an explicit simplifying assumption.

Real ball-pitch friction can change the ball's spin during impact. Pandey and Rao (2020), for example, found that the coefficient of friction affects the ball's exit spin.

Model 4B does not attempt to calculate that change because doing so would require a more advanced rigid-body impact model involving torque, moment of inertia, and angular impulse.

---

# Motion After the Bounce

Immediately after the bounce, the ball has:

- reversed and reduced vertical velocity
- changed sideways velocity because of pitch friction
- unchanged forward velocity
- unchanged angular velocity

Once the ball leaves the pitch, friction no longer acts.

The normal flight forces resume:

$$
\boxed{
\vec F_{\text{net}}
=
\vec F_g+\vec F_D+\vec F_M
}
$$

Gravity, drag, and the Magnus effect therefore continue to influence the post-bounce trajectory.

---

## Second Pitch Contact

When:

$$
y\leq0
$$

for the second time:

$$
y=0
$$

and the simulation stops.

---

# Expected Model Output

Model 4B should show:

- Magnus-induced movement during the initial flight
- a vertical bounce when the ball reaches the pitch
- an instantaneous change in sideways velocity caused by the simplified frictional impulse
- visible sideways turn after the bounce
- continued gravity, drag, and Magnus effects during the post-bounce flight

The direction of the post-bounce turn should reverse if the spin direction parameter \(s\) is reversed.

Increasing the coefficient of friction \(\mu\) should produce a larger sideways velocity change in this simplified model.

Model 4B therefore demonstrates the two major stages of spin bowling:

$$
\boxed{
\text{spin-induced aerodynamic movement in flight}
\rightarrow
\text{friction-induced turn after pitching}
}
$$

---

# Model Limitations

Model 4B is intentionally simplified.

It does not model:

- the detailed deformation of the cricket ball or pitch
- changing contact forces during impact
- torque during the bounce
- changes in angular velocity caused by pitch friction
- rolling versus sliding transitions
- changes in forward velocity caused by pitch friction
- detailed differences between pitch surfaces

These effects require a more advanced rigid-body/contact-mechanics treatment.

The simplified model is intended to demonstrate the primary physical idea that friction between a spinning cricket ball and the pitch can produce post-bounce lateral deviation.

---

# Sources

## Spin Bowling and Magnus Effect

Chinagodaba, B., Alway, P., Bull, H., Yadav, N., & King, M. (2026). *Sensitivity of Ball Landing Location to Variations in Release Velocity in Cricket Spin Bowling*. Applied Sciences, 16(8), 3991. DOI: 10.3390/app16083991.

Used for:

- the Magnus-force equation
- the gravity + drag + Magnus flight model
- the Magnus coefficient used in Model 4A and 4B

## Cricket Ball-Pitch Friction

Pandey, A., & Rao, C. L. (2020). *Numerical simulation of ball-pitch impact in cricket*. International Journal of Advances in Engineering Sciences and Applied Mathematics, 12, 39–43. DOI: 10.1007/s12572-020-00269-3.

Used for:

- the role of friction during cricket ball-pitch impact
- the \(\mu=0.30\) baseline
- evidence that friction influences rebound angle, rebound velocity, and exit spin

## Sliding Friction Impulse

Doménech-Carbó, A. (2024). *Independent friction-restitution modeling of collisions: application to planar sphere rebound on a massive surface*. European Journal of Physics, 45, 065004. DOI: 10.1088/1361-6404/ad7c99.

Used for:

- impulse-based modeling of short collisions
- the sliding-regime relationship

$$
J_f=\mu J_n
$$

- combining friction and restitution in a simplified sphere-surface collision