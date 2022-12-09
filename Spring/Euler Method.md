Here is a function that uses Euler's method to model the movement of a spring:
```lua
function spring_movement(spring_constant, mass, displacement, velocity, dt)
    local force = spring_constant * displacement
    local acceleration = force / mass

    -- Update position using Euler's method
    displacement = displacement + velocity * dt
    velocity = velocity + acceleration * dt

    return displacement, velocity
end
```
This function takes in five arguments: the spring constant, the mass of the object attached to the spring, the displacement of the spring from its equilibrium position, the velocity of the object, and the time step (`dt`) to use in the Euler's method calculation. It first calculates the force on the spring and the acceleration of the object using the same equations as in the previous example. It then uses Euler's method to update the displacement and velocity of the object for the given time step.

To model the full movement of the spring, you would need to call this function repeatedly, using the updated displacement and velocity values as the input for the next time step. You would also need to keep track of the time passed to know when to stop the simulation.

Here is an example of how you could use this function to model the movement of a spring over time:
```lua
-- Set initial values
local spring_constant = 10
local mass = 2
local displacement = 1
local velocity = 0
local dt = 0.1

-- Set maximum time to simulate
local max_time = 10

-- Set up variables to store the results
local results = {}

-- Simulate spring movement over time
for t = 0, max_time, dt do
    -- Calculate new displacement and velocity using Euler's method
    displacement, velocity = spring_movement(spring_constant, mass, displacement, velocity, dt)

    -- Store the results
    results[t] = {displacement = displacement, velocity = velocity}
end

-- Print the results
for t, result in pairs(results) do
    print(string.format("At time t = %.1f, displacement = %.2f, velocity = %.2f", t, result.displacement, result.velocity))
end
```
This code sets up the initial values for the spring constant, mass, displacement, and velocity, as well as the time step to use in the Euler's method calculation. It then simulates the movement of the spring over time, using the `spring_movement` function to update the displacement and velocity at each time step. Finally, it prints out the results of the simulation.

Note that this is a very simple model of spring movement and does not take into account other factors that can affect the movement of a spring, such as damping or external forces. It is also using a very basic numerical integration method that can be less accurate than other methods, such as Runge-Kutta. However, it should give you a basic idea of how to model spring movement in Lua using Euler's method.

