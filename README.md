# Pong
#This is my second project  I made and the first time I have ever used the turtle module. Although this may be over-commented, this is for my future knowledge and to understand every command when I refer back to my program. 
# Simple pong in python 
# Marc Davila

import turtle # Imports a module which allows to create pictures and shapes

start = turtle.Screen() # Creates a screen
start.title("Pong") # Title called Pong
start.bgcolor('black') # Background color black
start.setup(width = 800, height = 600) # Makes the screen 
start.tracer(0) 

# Paddle 1
pd_1 = turtle.Turtle() # From the module create a class and store it into pd_1.
pd_1.speed(0) # Speed of the object is 0 so it does not move on its own.
pd_1.shape('square') # First paddle shape is square.
pd_1.shapesize(stretch_wid =5, stretch_len=1 ) # Then convert it into a rectangle.
pd_1.color('white') # Makes the paddle white.
pd_1.penup() # Usually, turtle has pendown, causing lines to follow where object goes.
pd_1.goto(-350,0) # Make the starting point x = -350 and y = 0.

# Paddle 2
pd_2 = turtle.Turtle() # From the module create a class and store it in pd_2.
pd_2.speed(0) # Speed of the object is 0 so it does not move on its own.
pd_2.shape('square') # Shape is square.
pd_2.color('white') # Make the second paddle white. 
pd_2.shapesize(stretch_wid =5, stretch_len=1 ) #Transforms second square into a rectangle.
pd_2.penup() # Usually, turtle has pendown, causing lines to follow where object goes.
pd_2.goto(350,0) # Make the starting point x = 350 and y = 0.

# Ball
ball = turtle.Turtle() # Create a class from module and store it into ball.
ball.speed(0) # Speed of object is 0 so it does not move on its own.
ball.shape('circle') # Make the shape into a circle.
ball.color('white') # Make the color of the ball white.
ball.penup() # Usually, turtle has pendown, causing lines to follow where object goes.
ball.goto(0,0) # Put ball at x = 0 and y = 0.
ballspeed = 2.5 # Change the speed of the ball to 2.5.
ball.dx = ballspeed # Change the speed of the ball to 2.5 from the x direction.
ball.dy = ballspeed # Change the speed of the ball to 2.5 from the y direction.

#Score
score_1 = 0 # Starting score for the left player.
score_2 = 0 # Starting score for the right player.

# Pen
pen = turtle.Turtle() # Create a class from module and store it into pen.
pen.speed(0) # Speed of object is 0 so it does not move on its own.
pen.color('white') # Make the color of the object white.
pen.penup() # Usually, turtle has pendown, causing lines to follow where object goes.
pen.hideturtle() # Hides the object from the screen.
pen.goto(0,260) # Teleports to x = 0 and y = 260/ Top of the screen. 
pen.write("Player 1: {} Player2: {}".format(score_1, score_2), align = 'center', font= ('Courier', 24, 'normal'))
# Line 53 writes the players scores, additionally, aligns the text to the center and makes the font courier.


# Functions
def pd1_u():
    y = pd_1.ycor() # Create a variable to the y turtle's current position.
    y += 20 # Add the y coordinate by 20/ to move the first paddle.
    pd_1.sety(y) # Set the paddle to new position.

def pd1_d():
    y = pd_1.ycor() # Create a variable to the y turtle's current position.
    y -= 20 # Subtract the y coordinate by 20/ to move the first paddle.
    pd_1.sety(y) # Set the paddle to new position.

def pd2_u():
    y = pd_2.ycor() # Create a variable to the y turtle's current position.
    y += 20 # Add the y coordinate by 20/ to move the second paddle.
    pd_2.sety(y) # Set the paddle to new position.

def pd2_d():
    y = pd_2.ycor()
    y -= 20 # Subtract the y coordinate by 20/ to move the second paddle.
    pd_2.sety(y) # Set the paddle to new position.

# Keyboard Binding
start.listen() # Look for when a button is pressed
start.onkeypress(pd1_u, 'w') # Play function pd1_u if w is pressed.
start.onkeypress(pd1_d, 's') # Play function pd1_u if s is pressed.
start.onkeypress(pd2_u, 'Up') # Play function pd2_u if Up arrow is pressed.
start.onkeypress(pd2_d, 'Down') # Play function pd2_u if Down arrow is pressed.

# Keeps the game going
while True:
    start.update() # Update the game

    # Ball movement
    ball.setx(ball.xcor() + ball.dx) # Create the ball movement for x coordinates
    ball.sety(ball.ycor() + ball.dy) # Create the ball movement for y coordinates

    # Check for border 
    if ball.ycor() > 290: # Bounces back the ball from the ceiling
        ball.sety(290)
        ball.dy *= -1

    if ball.ycor() < -290: # Bounces back the ball from the floor
        ball.sety(-290)
        ball.dy *= -1

    if ball.xcor() > 390:
        ballspeed = 2.5 # Put speed back to 2.5
        ball.goto(0,0) # Restart Game
        ball.dx *= -1 # Changes the direction
        score_1 += 1 # Add point
        pen.clear()
        pen.write("Player 1: {} Player2: {}".format(score_1, score_2), align = 'center', font= ('Courier', 24, 'normal'))
    # Line 107 Rewrite the player board and update the score

    if ball.xcor() < -390:
        ballspeed = 2.5 # Put speed back to 2.5
        ball.goto(0,0) # Restart Game
        ball.dx *= -1 # Changes the direction
        score_2 += 1 # Add point
        pen.clear()
        pen.write("Player 1: {} Player2: {}".format(score_1, score_2), align = 'center', font= ('Courier', 24, 'normal')) 
        # Line 116 Rewrite the player board and update the score

    # Paddle Collisions
    if (ball.xcor() > 340 and ball.xcor() < 350)  and (ball.ycor() < pd_2.ycor() + 50 and ball.ycor() > pd_2.ycor() - 50):
        ball.setx(340)
        ball.dx *= -1 # Changes the direction
        ballspeed = ballspeed + 0.5 # Increases the speed

    if (ball.xcor()  < -340 and ball.xcor() > -350)  and (ball.ycor() < pd_1.ycor() + 50 and ball.ycor() > pd_1.ycor() - 50):
        ball.setx(-340)
        ball.dx *= -1 # Changes the direction
        ballspeed = ballspeed + 0.5 # Increases the speed
