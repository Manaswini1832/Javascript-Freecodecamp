# Javascript freecodecamp

This repo has been created to record what I'm learning from the javascript section of freecodecamp.
I am creating this after having finished the first module and half of the second module.

## Class syntax to define a constructor function

Class keyword declares a new function, to which a constructor is added. This constructor is invoked when new is called to create a new object.

```
class SpaceShuttle {
  constructor(targetPlanet) {
    this.targetPlanet = targetPlanet;
  }
}
const zeus = new SpaceShuttle('Jupiter');
```
