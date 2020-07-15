# Practical Scripting with Python
## UNO Summer Techademy

## Objectives
- Add elements to our Turtle Graphics
  - Random placement?
  - Random shapes?
  - Functions to do this

## Functions to change our turtle.

```
import random

def randomMove(myTurtle):
  myTurtle.up() #pickup pen
  # How do we pick a new random spot?

  myTurtle.down() #done moving, pen down.


def randomShape(myTurtle):
  #use some of the shapes we built last time.
  #add any new shapes?
  choice = random.randint(1, 4)
  if choice == 1:
    drawSquare(myTurtle, 100)

def randomColor(myTurtle):
  #make a list of colors
  #pick a color
  #set my turtle to be that color

```

## Value Returning Functions
We have made functions for the turtle to do different tasks, now we want to make a function that can do a task and give us an answer.

### CodingBat
CodingBat is a website that allows us to practice unit tested value returning functions.
[https://codingbat.com/python/Warmup-1](https://codingbat.com/python/Warmup-1)


### Program Development
At this point, you should be able to look at complete functions and tell what they do. Also, if you have been doing the exercises, you have written some small functions. As you write larger functions, you might start to have more difficulty, especially with runtime and semantic errors.

To deal with increasingly complex programs, we are going to suggest a technique called incremental development. The goal of incremental development is to avoid long debugging sessions by adding and testing only a small amount of code at a time.

As an example, suppose you want to find the distance between two points, given by the coordinates (x1, y1) and (x2, y2). By the Pythagorean theorem, the distance is:

![Distance Formula](distance_formula.png)

The first step is to consider what a distance function should look like in Python. In other words, what are the inputs (parameters) and what is the output (return value)?

In this case, the two points are the inputs, which we can represent using four parameters. The return value is the distance, which is a floating-point value.

Already we can write an outline of the function that captures our thinking so far.
```
def distance(x1, y1, x2, y2):
  return 0.0
```
Obviously, this version of the function doesn’t compute distances; it always returns zero. But it is syntactically correct, and it will run, which means that we can test it before we make it more complicated.

For the second test the horizontal distance equals 3 and the vertical distance equals 4; that way, the result is 5 (the hypotenuse of a 3-4-5 triangle). For the third test, we have a 1-1-sqrt(2) triangle.

At this point we have confirmed that the function is syntactically correct, and we can start adding lines of code. After each incremental change, we test the function again. If an error occurs at any point, we know where it must be — in the last line we added.

A logical first step in the computation is to find the differences x2- x1 and y2- y1. We will store those values in temporary variables named dx and dy.

```
def distance(x1, y1, x2, y2):
  dx = x2 - x1
  dy = y2 - y1
  return 0.0
```
Next we compute the sum of squares of dx and dy.
```
def distance(x1, y1, x2, y2):
  dx = x2 - x1
  dy = y2 - y1
  dsquared = dx**2 + dy**2
  return 0.0
```
Finally, we have our working function we can test.
```
def distance(x1, y1, x2, y2):
  dx = x2 - x1
  dy = y2 - y1
  dsquared = dx**2 + dy**2
  result = dsquared**0.5
  return result
```

### Composition
As we have already seen, you can call one function from within another. This ability to build functions by using other functions is called composition.

As an example, we’ll write a function that takes two points, the center of the circle and a point on the perimeter, and computes the area of the circle.

Assume that the center point is stored in the variables xc and yc, and the perimeter point is in xp and yp. The first step is to find the radius of the circle, which is the distance between the two points. Fortunately, we’ve just written a function, distance, that does just that, so now all we have to do is use it:
```
radius = distance(xc, yc, xp, yp)
```
The second step is to find the area of a circle with that radius and return it. Again we will use one of our earlier functions:
```
result = area(radius)
return result
```
Wrapping that up in a function, we get:
```
def distance(x1, y1, x2, y2):
  dx = x2 - x1
  dy = y2 - y1
  dsquared = dx**2 + dy**2
  result = dsquared**0.5
  return result

def area(radius):
  b = 3.14159 * radius**2
  return b

def area2(xc, yc, xp, yp):
  radius = distance(xc, yc, xp, yp)
  result = area(radius)
  return result

print(area2(0,0,1,1))
```
We called this function area2 to distinguish it from the area function defined earlier. There can only be one function with a given name within a module.

Note that we could have written the composition without storing the intermediate results.
```
def area2(xc, yc, xp, yp):
  return area(distance(xc, yc, xp, yp))
```

## Exploring further
How can we use this idea of problem deconstruction to solve other problems we might experience?
- What other math problems might we solve?
- Are there other tasks that could be broken up into smaller pieces?
