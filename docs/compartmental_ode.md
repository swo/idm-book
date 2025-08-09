# Compartmental ordinary differential equation models

- People use "SIR" to roughly mean this. But "SIR" is about disease states, not necessarily ODEs.
- A "compartmental" model means that you only need to track one thing about each individual, which is what compartment they are in. That completely specifies the state of the model.
- In a naive ODE, this means that you have exponential waiting times in each compartment. This is memoryless.
- You can have more complex state. E.g., if you have chains or matrices of compartments representing a single disease state, to get a different waiting time distribution.
- Or you can have multiple compartments that represent different people.
