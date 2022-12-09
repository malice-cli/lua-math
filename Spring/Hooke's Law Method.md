```lua
function spring_movement(spring_constant, mass, displacement)
    local force = spring_constant * displacement
    local acceleration = force / mass
    return acceleration
end
```
This function takes in three arguments: the spring constant, the mass of the object attached to the spring, and the displacement of the spring from its equilibrium position. It calculates the force on the spring using Hooke's Law (`F = kx`, where `F` is the force, `k` is the spring constant, and `x` is the displacement), and then uses Newton's Second Law (`F = ma`, where `F` is the force, `m` is the mass, and `a` is the acceleration) to calculate the acceleration of the object attached to the spring.

This function only calculates the acceleration of the object attached to the spring. To model the full movement of the spring, you would need to use this acceleration to update the position and velocity of the object over time using a numerical integration method, such as Euler's method.