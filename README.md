# TheUnchartedBranch
Using the Advanced Kinematic Controller to recreate a scene from Uncharted


# Scripted Jumps: 17/05

Taking off from the latest AKC example, I added: 
* Block and Dodge Mechanics. To do so, the hitbox responsible for detecting hurt signals has various sub-states : normal, dodge and hurt. User input triggers an animation that informs this hurtbox to update its state. If during the animation a hit is registered, then the appropriate response is initiated (dodge, or block and inform opponent of the block). To help opponent detect these moments, a specific material replaces the usual when in these states. 

But, the main feature of this package is...

* The Scripted Jump ! Initially, the goal was to be able to reach remote ledges or specific points that would require an accuracy that the current controller don't meet. To do so, I created the `JumpBox` script. It holds informations in the custom class `ScriptedJumpData` about landing target point, jump velocity and additional height. 
    * A trigger is set wherever I want the area to be. On entering this trigger, the informations about the jump are passed to the move module. If the user asks for a jump while in this area, the trajectory is initalized. Otherwise, when the player exits the area, I remove these infos, and the player can jump again as before. 
    * To move the player along trajectory, I just solve $y = axx + bx + c$ where x goes from 0 to 1. I use initial jump position and target position to compute y during this movement. 
    * To land, when x > 0.95 say, I initiate the landing procedure and reset the jump data. And that's it ! 
    
Video at : https://youtu.be/fSLNErphs1g
