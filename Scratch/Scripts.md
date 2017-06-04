# Scripts

## Motion
* These blocks allow the sprite to move and rotate in space
Method Blocks
1. __Move _ steps__
	* Moves the selected sprite that many pixels in the direction the sprite is pointing
2. __Turn _ degrees__
	* Rotates the sprite that many degrees, or rather, changes the directon of the sprite that many degrees
3. __Point in direction__
	* Rotates the given point in the given direction
	* Useful if the current direction is not known
4. __Point towards__
	* Points the direction of the sprite towards the given point 
5. __Go to__
	* Goes to the selected point instantaneuosly 
6. __Glide__
	* Goes to the selected point while redrawing the sprite at each intermediary step
		* Basically makes it glide there
7. __Change x by__
	* Changes x by that much
	* Equivalent to x +=
8. __Change y by__
	* Changes y by that much
	* Equivalent to y += 
9. __If on edge, bounce__
	* If a sprite hits an edge, it begins traveling in a reflected direction
	* Useful for constantly moving elements
10. __Set rotation style__
	* 
	1. _Full Rotation:_ Visually points the sprite in the direction that it is facing
	2. _Left- Right Rotation:_ Only visually flips the sprite left or right
		* Rotates left if direction is (0, -180)
		* Rotates right if direction is (0, 180)
	3. _Don't rotate:_ Does not visually rotate the sprite at all
Variable Blocks
1. __X position__
	* Returns the current x position
2. __Y position__
	* Returns the current y position, in pixels
3. __Direction__
	* The direction in which the sprite is currently pointing. This is a cartesian system, in which the +y axis is 0, -x axis is -90, +x is 90 and -y is 180

## Looks


## Sound


## Pen


## Data
Allows the creation of variables or arrays

## Events
1. __When flag clicked__
	* Performs the below block once the green flag is clicked
2. __When _ key is clicked__
	* Performs the below block if the selected key is being pressed
	* Typically, Scratch only checks to see if the key is pressed once, so for games, we need to wrap this with a loop
3. __When this sprite is clicked__
	* Performs below block if the given sprite is clicked
4. __When backdrop switches to ___
	* Performs the below block when the backdrop of the selected layer changes to the selected one
5. __When loudness > ___
	* Performs below block when the loudness of the sound exceeds the selected value
6. __When I receive ___
	* Performs below block when there is a broadcast with the given value
7. __Broadcast ___
	* Broadcasts the given text
	* Broadcasting gives a way for different sprites to communicate with one another
8. __Broadcast _ and wait__
	* Broadcasts the given text, then halts the code block until any "_when I receive" blocks are finished executing

## Control
1. __Wait _ secs__
	* Halts the execution of the given code block for that many seconds
2. __Repeat _ times__
	* For loop
3. __Forever__
	* Infinite while loop
4. __If _ then ___
	* If block
5. __If _ then _ else__
	* If- else block
6. __Wait until__
	* Pausing the block's script until the given event occurs
7. __Repeat until__
	* 

## Sensing

## Operators

## More Blocks