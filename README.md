# class32
bunny game with sounds 


---

 the constructor() we are taking two parameters nlinks - number of links and
pointA - points of connection.
Using Composites.stack() function we create the multiple
rectangular bodies and store it in the rect variable. Using the Composites.chain() function we create the
chain of the rectangles.
And then using the Constraints.create() we add the constraints to the chain which connects all the bodies of the chain together like we have string in a necklace.
We have the break() function which helps us to break the chain.It simply makes the rope body null.




https://brm.io/matter-js/docs/classes/Composites.html

For our code we are only going to use the rope.js to create the rope and break() function to break the rope when the user clicks on the cut button(which will be added in upcoming classes).
Add rope.js in index.html
To create a rope we need two pieces of important information, first is how long our rope will be, and where we want to hang our rope.
To define the length of the rope, we define a number that creates those many sections in the rope. One section essentially is a rectangle, so you can imagine our rope to be multiple rectangles connected together.
Next, we need the point where we are going to hang the rope, which will be a certain x and y position on the canvas.


in the setup() function create an object from the Rope class.
While creating the object first we write the length of the rope which we will set as 6, and then the x and y position, x would be 245 and y as 30.

The next step is to call the rope.show() function in the draw() function so that we can see the rope hanging.
Now comes the fun part to create the fruit body and hang it with our rope.



in the setup function, we first create fruit_options for the fruit body. In the options, we are only defining the density of the fruit as 0.001.
Then we create a fruit body using the Bodies.circle() function.
In the function, we need to provide the x and y positions and the radius of the fruit along with fruit_options.
Once we create the body, we need to add this body in the composite, now what is a composite?
As you have seen in the visuals, a composite consists of multiple bodies within it. When we want multiple bodies to have the same properties such as shape and size and behave in a certain manner, we make a composite of these bodies.


the rope we are creating is made up of multiple rectangles, hence we call it a composite. But we also have to add our fruit in the same composite.
To add a body to the composite, we use the function,
Matter.Composite.add(name_of_composite, body_to_add).


Here the composite is a body of the Rope class, and we are adding the fruit to it.
To display this body, we will create a circle, using the ellipse function in the draw() function.
For the x and y positions of the circle, we will pass the x and y position values from the fruit body.


When you run the code, the fruit will appear at the position defined and will fall on the ground.


Because we have not added any constraint between the fruit body and the rope. They are part of the same composite but not attached to each other with any constraint.


we need to write the code to hang the fruit with our rope.
For this, we are going to use constraints.
If you remember our rope is made up of various rectangles to be more specific 6 rectangles, which we specified while creating the rope object.
We will create a constraint between the fruit body and the last rectangle of our rope.

We create the class for the constraint because in the future classes we will hang the fruit with multiple ropes.
To make our code clean, we will keep all the code related to creating the constraint in the link.js file.





the constraint is going to be between 2 bodies, the last body (rectangle) of the rope and the fruit body.
That is why in the link class when we write the constructor we need to keep 2 parameters as bodyA and bodyB.
We want to connect the fruit body at the last rectangle of the rope. So we will create a variable to get the index of the last rectangle(or element, composite can be assumed like an array)
That will be var lastlink = bodyA.body.bodies.length-2
The last element will be 2 less than the length because the index always starts from 0, and we also added fruit in the composite that increases the length 1. So to get the last element index we need to subtract the 2 from the length.
So the function bodyA is rope.body.bodies[lastlink].bodyB is the fruit.


We will create the constraint using the createConstraint()
function of the matter.js library.
To connect 2 bodies we also need to specify at which point, on the body of the constraint, is it going to be connected.
For both bodies or we can say pointA and pointB, which are the X and Y positions so, we will write these as x:0 and y:0.


We need to define two more parameters:
● The length of the constraint, which we also keep 0 for now.
● The stiffness, which we write as 0.01. This value of stiffness will prevent vibration of the constraint (Here vibration refers to the small movements in the rope). So that our constraint stays stable.

the constraint is complete, we will add this to our world.
But before we run the code, we need to create the object of the link() class in the sketch.js file and pass the 2 bodies.
To create the object, first declare a variable as var fruit_con;
In the setup function we will create the object and assign it to the fruit_con variable;
While creating the object of the class, we need to pass the rope and the fruit as the parameters in the Link() class object.

