---
title: Space Shooter Game
layout: lesson
---

<script>
$(document).ready(function() {
  $('pre > code').each(function(i, block) {
    $(this).addClass('python');
    hljs.highlightBlock(block);
  });
});
</script>

<div style="text-align: center">
<img src="001.png" alt="Screenshot" />
</div>

## Introduction

In this lesson, you will be creating a 2D scroller game where the player
controls a space ship, and has to shoot as many aliens as possible before they
run out of lives.

You will be using `python` and `pygame` to create this game.

<div class="message-box task">
  <div class="title">Task</div>
  <div class="inner">
    Create a new folder where we will store everything for the game. Call it
    something like <code>space_game</code>.
  </div>
</div>

### Download Files

Here are the files that you need to download to use in your game.

* [`alien_1.png`](downloads/alien_1.png)
* [`bullet.png`](downloads/bullet.png)
* [`ship_down.png`](downloads/ship_down.png)
* [`ship_normal.png`](downloads/ship_normal.png)
* [`ship_up.png`](downloads/ship_up.png)
* [`stars_1.png`](downloads/stars_1.png)
* [`stars_2.png`](downloads/stars_2.png)

*Attribution and copyright for these images can be found on the [lesson
details page](../).*

<div class="message-box task">
  <div class="title">Task</div>
  <div class="message-inner">
    Download each of these files into the new folder you just created, but
    don't change their names.
  </div>
</div>

## Understanding Screens

Throughout the development of the game, we will be interacting with the
computer screen. Computer screens are made up of something called **pixels**,
a pixel is a very very tiny dot on the screen that can be many different
colours. Pixels of a computer screen are arranged into a rectangular grid, and
they work the exact same way as a television. A typical television will be
`1,920` pixels wide and `1,080` pixels tall, which means that it has
`2,073,600` pixels filling the whole screen.

### How movement on a screen work (frames)

To make it seem like things move on a computer screen or a television, what
happens is that the image changes many times a second, to trick our eyes into
thinking that things are moving. The number of times the picture changes every
second is called the **framerate**.

When we create our game, we will have a game **window**, which will be a
rectangular area, a certain number of pixels wide and high, which we will draw
to. When we want to show something moving in the window, we will re-draw the
entire window, and move the objects slightly, a certain number of times per
second.

## Getting Started

<div class="message-box task">
  <div class="title">Task</div>
  <div class="message-inner">
    Create a new python file called <code>game.py</code> in your python text
    editor, enter the following code, and save the file.
  </div>
</div>

    import pygame
    import sys

    pygame.init()

    window = pygame.display.set_mode((800, 500))
    clock = pygame.time.Clock()

    while True:

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()

        clock.tick(50)

<div class="message-box note">
  <div class="title">Note</div>
  <div class="message-inner">
    Pay very close attention to the amount of space before the code on each
    line. This is called indentation.
  </div>
</div>

<div class="message-box run">
  <div class="title">Run Your Code</div>
  <div class="message-inner">
    Try running your code now. You do this by typing <code>python
    game.py</code> from inside your terminal. (Make sure that your terminal is
    in the same folder that all your game files are in).
  </div>
</div>

If everything is working, a new black window should have appeared with nothing
inside. This is going to be our game screen, and we will start adding things to
it.

<div class="message-box note">
  <div class="title">Remember</div>
  <div class="message-inner">
    If you have run into a problem, ask your teacher or a helper before
    continuing.
  </div>
</div>

## Explaining The Starting Code

Now that we have the starting code for our game, lets go through and see what
each bit does.

    import pygame
    import sys

These first two lines tell python that we want to need to use some extra cod
from outside of our `game.py` file. In particular we want to use `pygame` and
`sys` at the moment. These are called `modules`.

We are going to use the `pygame` module a lot in this project.

    pygame.init()

This line tells `pygame` to make sure that everything is ready for us to use.

    window = pygame.display.set_mode((800, 500))

There are a few important things going on on this line. One of the first things
you should notice is that there is an equals `=` sign. What an equals sign
allows us to to is create variables.

A variable is like a **box** in our program that we can use to store stuff in,
and every variable has a name. If we write this code:

    my_variable = 4

... what we have done is create a new variable, a new box, and given it the
name `my_variable`. We've also put the number `4` inside it.

If we write this code:

    another_variable = 20
    another_variable = 21

... then we have created a variable called `another_variable`, given it the
value `20`, and then changed it straight away by giving it the value `21`.

Let's have a look at the code we've already written again:

    window = pygame.display.set_mode((800, 500))

The part of the code to the right of the equals sign,
`pygame.display.set_mode((800, 500))`, basically tells `pygame` that we want
a window on the computer screen that is `800` pixels wide, and `500` pixels
tall, and this is what it returns. This means that after this line of code is
run, we have a variable called `window` (remember a variable is a box), and
inside that variable is a window that we can manipulate, by drawing things on
it.

The next line is a little bit simpler:

    clock = pygame.time.Clock()

What this does is create a variable called `clock`, and make the value of that
variable a new `Clock`. A `pygame` clock is important, because it allows us to
control the frame rate (remember, the frame rate is how many times the screen
changes per second). You will see how we use the clock very shortly.

The next part of the code is where the magic happens:

    while True:

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()

        clock.tick(50)

This is what we call our **event loop**. The first line `while True`, means "do
this forever". Every line under this line has some extra space at the start of
it, this is what's called **indentation**. This is important because it tells
python that these lines of code are **inside** the loop, which means every time
the loop runs, it will run all the code that has the correct amount of space at
the start.

We are going to use our event loop at the heart of our game, and we will run
the loop once for each time we want to create the next frame of our window.

Every time we want to create the next frame, we will:

* Check if the user has interacted with the window at all (for example pressed
  an arrow key, or closed the window).
* Update information about the objects on the screen.
* Draw a new frame from scratch.
* Display that frame in our window.

Finally, let's address the last bits of the code.

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()

We'll skip over an explanation for these three lines of code for now, but they
will be explained later on. For now, all you need to know is that it checks if
the user has closed the window, and if the window has been closed we close the
whole program.

        clock.tick(50)

Now this is a clever bit of code. Because computers are so fast, if we let the
event loop run without any limitation, it would run many many thousands of
times faster than we would like, because the number of times it runs per second
will determine what our framerate is. This means that things moving on the
screen will probably be moving much faster than we would like.

One of the first things you should notice about this line is that it starts
with the same name as the variable `clock` that we created earlier, that is
because it is actually using the value stored inside that variable. We created
a `pygame` clock, and saved it in the variable `clock`, and now we have used
it. This line of code makes our program pause (basically slows it down), so it
only runs as fast as we want it to. Because we gave it the value `50`, it will
make sure that our loop does not run more than `50` times per second, so that
our frame rate will also not be faster than `50` times per second.

Later on, when we have things moving on screen, you will have the opportunity
to experiment with the frame rate, and see what the effect of it is on your
game.

<div class="message-box task">
  <div class="title">Task: Experiment!</div>
  <div class="message-inner">
    Change the numbers for the line that tells <code>pygame</code> the width
    and height, and run your code each time you change it. Do this a few times.
    Remember to change the numbers back to what they were before you continue.
  </div>
</div>

## Adding a Space Ship

Now let's add our first image to the game.

<div class="message-box task">
  <div class="title">Task:</div>
  <div class="message-inner">
    <p>Add these lines of code to your program above the while loop:</p>
<pre><code>background = (0, 0, 0)
ship_image = pygame.image.load("ship_normal.png")</code></pre>
    <p>And add these lines of code above the clock tick, indented by
      <strong>four spaces</strong>.</p>
<pre><code>    window.fill(background)
    window.blit(ship_image, (0, 0))

    pygame.display.flip()</code></pre>
  </div>
</div>

Your code should now look like this:

    import pygame
    import sys

    pygame.init()

    window = pygame.display.set_mode((800, 500))
    clock = pygame.time.Clock()

    background = (0, 0, 0)
    ship_image = pygame.image.load("ship_normal.png")

    while True:

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()


        window.fill(background)
        window.blit(ship_image, (0, 0))

        pygame.display.flip()

        clock.tick(50)

<div class="message-box note">
  <div class="title">Note</div>
  <div class="message-inner">
    Python does not care how many blank lines there are between lines of code,
    but it can make it easier to read and understand what's going on.
  </div>
</div>

<div class="message-box run">
  <div class="title">Run Your Code</div>
  <div class="message-inner">
    <p>
    Try running your code now. If everything is working, you should now see
    a black window with a space ship in the top left, like this:
    </p>
    <p style="text-align: center;">
      <img src="002.png" alt="Space Ship in Corner" />
    </p>
  </div>
</div>

Lets have a look at what the code that we have added is doing:

    background = (0, 0, 0)
    ship_image = pygame.image.load("ship_normal.png")

The first line is creating a variable called `background`. The value of this
variable is 3 numbers grouped together, into something called a **tuple**. At
the moment, this variable is used in one place, on the line that says
`window.fill(background)`, which we will explain in a bit, and we will explain
what those numbers mean.

The second line is creating a variable called `ship_image`, and loading an
image file (specifically the one stored as `ship_normal.png`), and storing the
image inside that variable.

        window.fill(background)
        window.blit(ship_image, (0, 0))

        pygame.display.flip()

These lines of code are all making changes to what we can see in the window.
And because they are all **indented** by `4` spaces, they are **inside** the
`while` loop (our event loop), which means they are run once every frame.

The first line fills in the whole window with a specific colour, in this case,
the colour stored in the variable `background`, and that is what the **tuple**
is. The tuple `(0, 0, 0)` represents the colour black, but there are over
16 million colours you can choose from!

The way in which we describe a colour to a computer is with what's called `RGB`
(which stands for **R**ed, **G**reen and **B**lue). This is because each pixel
(in most computer screens) is made up of three smaller parts, each of which
emits a different colour light. One part emits **red** light, one part emits
**green** light, and another part emits **blue** light. This allows us to
display a wide range of colours for each pixel on a screen.

The tuple `(0, 0, 0)` means we want `0` red, `0` green and `0` blue, which is
how we get black, by displaying **no light at all!** Each number in a tuple
which describes a colour has to be between `0` and `255`, it can't be higher
than `255`, and it can't be lower than `0`. For example, if we wanted to
display as much red as we can, but no green and blue, the colour would be
`(255, 0, 0)`.

<div class="message-box task">
  <div class="title">Task: Experiment!</div>
  <div class="message-inner">
    <p>
      Change the numbers inside the <strong>tuple</strong> that we set the
      variable <code>background</code> to, and <strong>run your code each
      time</strong>. See what happens if all the numbers are really big, and
      what happens if they are really small.
    </p>
    <p>
      To really experiment, try adding numbers that are <strong>less
      than</strong> <code>0</code> (eg: <code>-10</code>), or numbers that are
      bigger than <code>255</code>. If you do this, you should see that your
      game <strong>CRASHES!</strong>.
    </p>
    <p>
      It might say something like this:
    </p>
<pre><code>Traceback (most recent call last):
  File "game.py", line 19, in &lt;module&gt;
    window.fill(black)
TypeError: invalid color argument</code></pre>
    <p>
      This means there is a <strong>bug</strong> in your program, and python is
      trying to tell you where the bug is so that you can fix it. When you
      write software and games, you will come accross lots of bugs that you
      will need to fix. This is a normal part of learning to program. Even the
      best programmers make mistakes and need to fix bugs they created on a
      daily basis.
    </p>
    <p>
      <strong>REMEMBER:</strong> Don't forget to change the colour back to
      black (or to a colour close to black) before continuing.
    </p>
  </div>
</div>

Lets get back to the code now:

        window.fill(background)
        window.blit(ship_image, (0, 0))

        pygame.display.flip()

The second line of code copies the image that we have loaded and stored in the
variable `ship_image`, and places it inside the window. You can see that when
we run the code, the ship is places in the top left hand corner of the screen.
The two numbers in brackets `(0, 0)` is what is telling `pygame` to do this.
This is another **tuple**, and this tuple is used to represent
**co-ordinates**. Specifically, these co-ordinates are the `x` and `y`
positions of where we want the image to be in our window.

* If we **increase** our `x` value, then the image would be more to the
  **right**.
* If we **increase** our `y` value, then the image would be further **down**
  the screen.

When `x` is `0` and `y` is `0`, then we mean the pixel that is furthest to the
**top** and furthest to the **left**.

Here's a diagram to explain:

<p style="text-align: center;">
  <img src="003.png" alt="x-y" />
</p>

This is a bit different to what you might be used to with drawing graphs at
school, where the **x-axix** is the same, but the **y-axis** goes up instead of
down. Unfortunately this is how `pygame`, and a lot of other computer graphics
work, and you will need to remember this difference.

<div class="message-box task">
  <div class="title">Task: Experiment!</div>
  <div class="message-inner">
    <p>
      Try changing the numbers for the line of code that copies the space ship
      to the window, and <strong>run your code</strong>. For example, changing
      it to <code>(300, 100)</code> results in this:
    </p>
    <p style="text-align: center;">
      <img src="004.png" alt="moved ship" />
    </p>
    <p>
      The ship has moved <code>300</code> pixels right, and <code>100</code>
      pixels down. This is because it now has an <code>x</code> value of
      <code>300</code> and a <code>y</code> value of <code>100</code>.
    </p>
    <p>
      If we instead use the co-ordinates <code>(-50, 50)</code>, we get this:
    </p>
    <p style="text-align: center;">
      <img src="005.png" alt="moved ship off screen" />
    </p>
    <p>
      You can see it has moved off screen.
    </p>
  </div>
</div>

Lets look at the final line of code we added:

        pygame.display.flip()

This line just tells `pygame` that, now that we have made changes to the
window, we would like it to be updated. The reason it doesn't update the window
automatically is because if we are doing a lot of changes, and if it takes a
long time, the user would see lots of un finished frames, when we are still
making changes to the window.

By requiring us to tell it when we have finished changing the window, `pygame`
can make sure that it updates the screen really quickly, all at once, so the
user never sees half-finished frames.

### Going over All the Code

Lets go over the whole program, and see if we can understand how it all works
together.

    import pygame
    import sys

    pygame.init()

    window = pygame.display.set_mode((800, 500))
    clock = pygame.time.Clock()

    background = (0, 0, 0)
    ship_image = pygame.image.load("ship_normal.png")

    while True:

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()


        window.fill(background)
        window.blit(ship_image, (0, 0))

        pygame.display.flip()

        clock.tick(50)

**What the code does:**

*Try and follow along with the code above so that you can make sure that you
understand what each line is doing.*

* We tell python that we want to use the `pygame` and `sys` modules.
* We tell `pygame` to set up.
* We create a new variable called `window`, and store a window object in there
  that we can manipulate.
* We create a new variable called `clock`, and store a `pygame` clock in there
  so that we can control the **framerate** of the game.
* We create a new variable called `background`, and store a **tuple** in there.
  We are going to use this **tuple** as a colour.
* We create a new variable called `ship_image`, and store the image of the
  space ship in it.
* We start a **loop**, that repeats forever, and will run once for every frame.
  Inside the loop:
  * We check if the user has closed the window, if the window is closed, we
    stop the program.
  * We fill the whole window with the colour stored in the variable
    `background`.
  * We copy the space ship image stored in `ship_image` to the window, at the
    top left of the screen.
  * We tell `pygame` that we have finished making changes to the window, and it
    should update the screen.
  * We make the loop pause for a short period of time so that our frame rate is
    not too high.

## Making the Space Ship Move

We are now going to use keyboard input to move the space ship around the
screen.

<div class="message-box task">
  <div class="title">Task:</div>
  <div class="message-inner">
    <p>Firstly add these two lines above the loop:</p>
<pre><code>ship_x = 0
ship_y = 0</code></pre>
  </div>
</div>

We are going to use these two variables to keep track of the space ship's
position: we will change them when the player presses the right keys, and use
their values to work out where to copy the space ship image to on the window.

<div class="message-box task">
  <div class="title">Task:</div>
  <div class="message-inner">
    <p>
      Underneath the code that checks if the user has closed the window, add
      this code:
    </p>
<pre><code>    pressed_keys = pygame.key.get_pressed()

    if pressed_keys[pygame.K_UP]:
        ship_y = ship_y - 10

    if pressed_keys[pygame.K_DOWN]:
        ship_y = ship_y + 10

    if pressed_keys[pygame.K_RIGHT]:
        ship_x = ship_x + 10

    if pressed_keys[pygame.K_LEFT]:
        ship_x = ship_x - 10</code></pre>
    <p>
      <strong>Note:</strong> make sure you indent it so that it is inside the
      loop!
    </p>
  </div>
</div>

This code that you have just added is what will change the position of the
space ship when you press certain keys on the keyboard.

    pressed_keys = pygame.key.get_pressed()

This line creates a variable called `pressed_keys`, which stores information on
which keys are currently being pressed by the player. Every time we run the
loop, we want to check if the user is currently pressing a particular key, and
if they are, then we will act accordingly.

The rest of the code uses things called **if statements**. If statements make
sure that certain parts of the code only run in certain situations.

Lets take a look at the first **if statement**:

    if pressed_keys[pygame.K_UP]:
        ship_y = ship_y - 10

Firstly, it uses the variable `pressed_keys` to check if the the user is
currently pressing the up key. If they are, then it runs the code which is
**indented** underneath it.

The code which is indented changes the value of the variable `ship_y` to
`ship_y - 10`, which means that `ship_y` will have a value of `1`0 less than it
had before: it will have been decreased.

The other 3 if statements work in the same way, **increasing** or
**decreasing** `ship_x` and `ship_y`.

<div class="message-box task">
  <div class="title">Task:</div>
  <div class="message-inner">
    <p>
      And finally, we want to actually use the variables <code>ship_x</code>
      and <code>ship_y</code> in the part of our code that copies the space
      ship image to the window. SO change this line of code:
    </p>
    <pre><code>    window.blit(ship_image, (0, 0))</code></pre>
    <p>
      To this:
    </p>
    <pre><code>    window.blit(ship_image, (ship_x, ship_y))</code></pre>
  </div>
</div>

<div class="message-box run">
  <div class="title">Run Your Code</div>
  <div class="message-inner">
    <p>
      Try running your code now. If everything is working, you should be able
      to press the arrow keys on your keyboard to move the space ship in the
      correct direction for each key.
    </p>
    <p>
      You will notice that it is very easy to make the space ship go off the
      edge of the window, this is probably something we want to fix later
      on&hellip;
    </p>
  </div>
</div>

<div class="message-box task">
  <div class="title">Task: Experiment!</div>
  <div class="message-inner">
    <p>
      What happens if you press multiple keys at the same time? What about if
      you press <strong>up</strong> and <strong>down</strong> at the same time?
    </p>
  </div>
</div>

<div class="message-box task">
  <div class="title">Task: Experiment!</div>
  <div class="message-inner">
    <p>
      Change the amount that we modify <code>ship_x</code> and
      <code>ship_y</code> by from <code>10</code> to something else. What
      happens if you have different numbers for different directions? Don't
      forget to <strong>run your code</strong> to find out!
    </p>
  </div>
</div>

<div class="message-box task">
  <div class="title">Task: Experiment!</div>
  <div class="message-inner">
    <p>
      Now that we have movement in our game, try changing the
      <strong>framerate</strong> of our game, and see what effect that has on
      our game.
    </p>
    <p>
      <strong>Remember:</strong> This is the code that looks like
      <code>clock.tick(50)</code>.
    </p>
  </div>
</div>




























<div class="message-box note">
  <div class="title">Work in Progress!</div>
  <div class="message-inner">
    <p>
      I have not yet finished writing this lesson. Thank you for your eagerness
      though. This page is being updated constantly.
    </p>
    <p>
      In the mean time, if you are interested in teaching python to students, I
      would recommend <a href="http://projects.codeclub.org.uk/">CodeClub's</a>
      resources.
    </p>
  </div>
</div>
