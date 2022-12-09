```lua
function spring_movement(spring_constant, mass, displacement, velocity, dt)
    local function f(displacement, velocity)
        local force = spring_constant * displacement
        local acceleration = force / mass
        return velocity, acceleration
    end

    local k1_displacement, k1_velocity = f(displacement, velocity)
    local k2_displacement, k2_velocity = f(displacement + dt/2 * k1_displacement, velocity + dt/2 * k1_velocity)
    local k3_displacement, k3_velocity = f(displacement + dt/2 * k2_displacement, velocity + dt/2 * k2_velocity)
    local k4_displacement, k4_velocity = f(displacement + dt * k3_displacement, velocity + dt * k3_velocity)

    local new_displacement = displacement + dt/6 * (k1_displacement + 2 * k2_displacement + 2 * k3_displacement + k4_displacement)
    local new_velocity = velocity + dt/6 * (k1_velocity + 2 * k2_velocity + 2 * k3_velocity + k4_velocity)

    return new_displacement, new_velocity
end
```
This function takes in five arguments: the spring constant, the mass of the object attached to the spring, the displacement of the spring from its equilibrium position, the velocity of the object, and the time step (`dt`) to use in the Runge-Kutta calculation. It defines an auxiliary function `f` that calculates the velocity and acceleration of the object based on the given displacement and velocity. It then uses the fourth-order Runge-Kutta method to update the displacement and velocity of the object for the given time step.

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
    -- Calculate new displacement and velocity using Runge-Kutta
    displacement, velocity = spring_movement(spring_constant, mass, displacement, velocity, dt)

    -- Store the results
    results[t] = {displacement = displacement, velocity = velocity}
end

-- Print the results
for t, result in pairs(results) do
    print(string.format("At time t = %.1f, displacement = %.2f, velocity = %.2f", t, result.displacement, result.velocity))
end
```
