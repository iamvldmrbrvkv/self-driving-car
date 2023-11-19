# self-driving-car
[Codecademy](https://www.codecademy.com/learn) [TypeScript](https://www.typescriptlang.org/) project.

## Self Driving Car
Self-driving cars are set to be the next revolution in the automotive industry. The idea is simple: create a vehicle that can see the world and react to it as a human driver would, but the implementation is fraught with obstacles. You are tasked with creating a program that will allow a car to react to obstacles in the road.

To accomplish this, you’ll use your knowledge of TypeScript object types to apply types to a variety of classes, properties, and methods. Start your engine and let’s hit the road!

### Start the engine
1. Let’s inspect the files that currently exist:

- index.ts: The file we’ll use to write a self-driving car program.
- computer-vision.ts: Contains a function that will generate random obstacles for our car to avoid.
- tsconfig.json: Defines the rules for TypeScript to compile code into JavaScript.

Take a moment to look over these files.

As we work on this program, it will be important that we keep our code organized. In general, there are going to be three “sections” of code: a section for types, a section for classes, and a section for execution. As you work, keep in mind what you’re coding and group your code accordingly.

2. To create this program, we’re going to create a class named Car that we will make autonomous by adding typed properties and methods to it. By the end of the program, we’ll have a Car that can take control of steering and react to obstacles.

Start by declaring a class named Car.

3. Declare an interface named AutonomousCar. It should have one optional type member named .isRunning of type boolean.

4. Apply the AutonomousCar type to the Car class using the implements keyword.

5. Our goal now is to get the car running. We’ll do that by passing in a value named .isRunning when we instantiate a new instance of the Car class later on.

Inside the Car class, declare a property named .isRunning, without any value.

6. To pass in a value for .isRunning when our class gets instantiated, we’ll need to write a constructor method that takes in a configuration object. Then we can associate this.isRunning with the .isRunning value that gets passed in.

In the Car class, underneath the .isRunning property you declared, write a constructor() method that takes in a parameter named props (short for “properties”).

7. If you hover your mouse over the props argument, you’ll notice that one of the errors listed is that props is of type any. To make this car as safe as possible, let’s create a type for it.

Above the Car class, declare an interface named AutonomousCarProps. It should have one type member, .isRunning, which is an optional boolean value.

8. Back in the Car class, apply the AutonomousCarProps type to the props parameter on the constructor() method.

9. Now that props has a type, let’s do something with it.

Inside the body of the constructor() method on the Car class, assign this.isRunning to the .isRunning property on props.

This way, we can instantiate a new instance of Car with an .isRunning argument, and the Car class can access this.isRunning.

10. Let’s verify that our Car is able to set its .isRunning variable.

Underneath the Car class, declare a variable named autonomousCar and set it equal to a new instance of the Car class. When you instantiate the Car class, pass in an object with the property .isRunning as true.

11. Underneath your autonomousCar variable, use console.log() to print the .isRunning property on autonomousCar.

Save your code, run tsc, then node index.js in the terminal to see the result. You should see true print as the output.

### Respond to events
12. Now that we can set the Car‘s .isRunning property, let’s add a method that will eventually respond to events. We’re going to add a .respond() method to Car to accomplish this.

Over the next few tasks, we will first add .respond() to our AutonomousCar interface, then we’ll add a .respond() method to Car to match our type. Finally, we’ll call .respond() to make sure it works as we expect.

Start by adding a required .respond() type member to the AutonomousCar interface. It should be a function type that has one parameter named events. We’ll define the type of events in the next task, so leave it as an any type for now. The .respond() method should return void.

13. If we hover our mouse over the events parameter we just wrote, we’ll see events is of type any, so let’s define it. In our program, we get events from computer-vision.ts. This is a function that generates faux/fake obstacles that we’ll eventually want our car to react to. The getObstacleEvents() function can return an object like this:
```js
{
  'ObstacleLeft': true, 
  'ObstacleRight': false
}
```
While this function returns these two keys at the moment ('ObstacleLeft' and 'ObstacleRight'), it may return different keys in the future.

Declare a new interface named Events. Use an index signature to allow this type to have any string as each key, with all the keys having a boolean typed value.

14. Apply the Events type to the events parameter on the AutonomousCar type.

15. If we hover our mouse over Car, TypeScript let’s us know there’s an error since Car does not contain a .respond() method. Let’s address that by adding one.

Add a .respond() method inside the Car class, below the constructor() function, that takes one parameter named events of type Events.

16. Inside the .respond() method, we want the car to only respond to events when .isRunning is truthy.

Write a conditional inside the body of the .respond() method that checks if the car is not running, by checking the value of this.isRunning. If it’s not running, return a console.log() that prints a statement that the car is off.

17. It’s time to make sure our .respond() method works as we expect.

At the bottom of your program, replace the console.log() with a call to the autonomousCar variable’s .respond() method. Since .respond() requires an events parameter of type Events, provide getObstacleEvents() as its argument.

Then save your code, run tsc, and then node index.js to see the result. You should see nothing print if .isRunning is set to true, and you should see your message print if .isRunning is false.

### Add steering
18. Now that our Car can begin to respond to events, let’s add some controls that can react to different events. In this section, we’re going to add a few types to define a steering control. Then we’ll create a class that handles steering. Then we’ll instantiate a steering instance and pass it to the Car so that our self-driving car can steer around obstacles.

Begin by creating an interface named Control. The interface should have one type member named execute() that is a function type with a parameter named command of type string, and a return type of void.

This type and its type member will allow us to enforce that all controls for our cars must have an .execute() method.

19. Declare another interface named Steering. This interface should copy all the type members of Control using the extends keyword.

Inside the Steering interface, there should be one type member named turn(). It should be a function type that has one parameter named direction of type string that returns void.

20. With our types defined, let’s make a class to handle steering.

Declare a class named SteeringControl that implements the Steering type.

21. Since we applied the Steering type to the SteeringControl class, we need to give it both .execute() and .turn() methods.

Declare a method named .execute() inside the SteeringControl class. It should have one parameter named command typed as a string.

Inside the .execute() method, use console.log() to interpolate the string 'Executing:' followed by the command parameter.

22. Underneath the .execute() method inside the SteeringControl class, declare another method named .turn(). It should have a parameter named direction of type string.

Inside the .turn() method, call this.execute(), with a string as its argument. The string should tell the steering control to “turn”, then it should interpolate the direction.

Later, when we call .turn() with an argument like “right”, we’ll want the resulting command line output to say something similar to 'Executing: turn right'.

23. Near the bottom of the program, right above the autonomousCar variable, instantiate an instance of the SteeringControl class so that we can test it to make sure it works. Then we’ll pass it to the Car class to let the car steer itself.

Declare a variable named steering and set it equal to a new instance of the SteeringControl class.

Once you’ve done so, test out the .turn() method on steering. Save your code, run tsc, then node index.js to see the output.

### Let the Car take the wheel
24. For a car to drive itself, it must steer itself. Therefore, we’ll want to pass steering into the Car class when we create a new instance of it. Before we pass it in, let’s update our types to include a type member for a steeringControl.

In the AutonomousCarProps, add a required type member named steeringControl of type Steering.

25. Now we need to declare a variable within the Car class that will hold our steeringControl value and attach it to this.

Inside the Car class, right below where .isRunning is declared, declare another property named .steeringControl. Its value should be undefined.

26. Inside the Car class’s constructor() method, add another assignment below the this.isRunning assignment to set the .steeringControl from props as the value of the .steeringControl on this.

27. Locate the autonomousCar variable we created before that instantiates a new Car instance. While creating a new instance, pass in a new property named steeringControl with a value of steering, which is an instance of the SteeringControl class.

### Steer around obstacles
28. We’ve given our Car class access to control steering. Now let’s instruct it how to do so.

Inside the Car class, there’s a .respond() method that takes in events. We typed these events earlier as type Events. Our goal is to take each individual event from events and allow the car to execute a steering command.

Inside .respond(), create an array of every key in events with the [Object.keys() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys).

Then use the .forEach() method to loop over each key using a callback function with a single eventKey parameter.

29. Before we issue any commands for our car to steer, we’ll want to make sure the event has a truthy value.

Inside the .forEach() method, write a conditional that checks if the eventKey on the events object is false. If it’s false, then immediately return.

30. After the conditional from the last task, let’s set rules for which way to turn for each type of event

Write a conditional that checks if the eventKey is equal to 'ObstacleLeft'. If it is, then call the .turn() method on this.steeringControl with an argument to turn “right”.

31. Underneath the conditional from the previous task, write another conditional to make the steering turn “left” when the eventKey is 'ObstacleRight'.

32. At the bottom of our program, make sure you’re passing in getObstacleEvents() into autonomousCar.respond().

Save your code, run tsc, and then node index.js to see the result. Run the program multiple times to see the self-driving car turn left and right.

33. We’re cruising! Now you can ride around in style while your car does your driving for you.

Take this project to the next level and practice your skills with these extra credit tasks:

- Write code that will call .respond() many times with new events to see a sequence of turns.
- Write code that allows the car to accelerate or decelerate based on the event. You could make this another type that extends the Control type.
- Add more types of events so your car can do things like ‘emergencyBrake’ or ‘parallelPark’.