# Models

Models in CraftStudio are 3D objects made of blocks. You can use models to create characters or objects for your game.

----
## Blocks

Each model block has several properties: name, position, orientation, block size, pivot offset and stretch.

The size defines how many pixels the block is made of on each axis. Changing the block size also increases the number of pixels it uses up on the drawing sheet.

The pivot offset is used to recenter the block around its origin. This will come in handy when you want to articulate a character to be able to animate it properly for instance.

Here is a set a blocks designed to create a character model. The painted blocks are represented in the painting pane on the lower left.  

![Modeling.png](https://bitbucket.org/repo/ey9q4X/images/389906609-Modeling.png)

----
## Painting

In order to paint model blocks, you need to lay out the block unwraps on the drawing sheet first. You can do that by selecting a model block in the 3D viewport then dragging around its unwrap in the left pane, all while in the Build tab.

Once you're done laying out your blocks, head over to the Paint tab to select colors and paint on the drawing sheet.

----
## Hierarchy

Blocks working together to make a model can also be arranged in hierarchies. This means that one block can be a "parent" to another block which is a "child". This arrangement causes child blocks to follow their parents, as if attached, even if they are not touching.

This works like many things do in the real world. Your arm is a "parent" to your hand. Your hand is a "parent" to five "child" fingers.

![Hierarchies.png](https://bitbucket.org/repo/ey9q4X/images/1959504135-Hierarchies.png)

CraftStudio blocks can have one or many children blocks, and children blocks can have children blocks of their own, just like the arm / hand / fingers example.
