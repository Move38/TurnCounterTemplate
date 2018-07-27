# TurnCounterTemplate #
A repository to store all information regarding a turn counter for multiplayer Blinks games 

The TurnCounterTemplate.ino contains a basic sketch that has one example model of how a turn-based player counter can work. It is a turn counter based off of the "Fracture" game for Blinks. 

Each Blink will have three states that roughly correspond with the phases of a player's turn: NOMINAL, FRACTURED, and RESOLVING. 

In this model, a player is represented by a specific color. When it is a certain player's turn, all Blinks will glow that player's color (ex. Player 1 is represented by blue. When it is Player 1's turn, all Blinks will be relaying the color blue on their 0 face). This is the NOMINAL state. Currently, for testing purposes, the template assumes 4 players in the game. 

A turn starts when one or more Blinks are separated from the other Blinks. The separated Blinks will enter the FRACTURED state due to having missing neighbors and glow white indicating their state. The Blinks they directly separated from also enter this state due to recognizing their neighbors got cut off, and enter the FRACTURED state as well. They will relay a message to all connecting Blinks to become FRACTURED as well (it is possible to visually witness the communication speed is one has enough Blinks). The FRACTURED state indictates the player is in the middle of their turn. 

When a FRACTURED Blink is reconnected to the other Blinks, they will enter a RESOLVING state. The RESOLVING state increments the total moves of the game so far and also signals the end of a player's turn. A Blink in the RESOLVING state will relay its RESOLVING state to all connecting Blinks. When a RESOLVING Blink is surrounded by either RESOLVING or NOMINAL Blinks, it itself becomes NOMINAL. Because of this, Blinks are only briefly in the RESOLVING state. 

Once all Blinks are in the NOMINAL state, they should indicate the next player's color on their 0 face. 

# Pending Issues #

While this turn counter template works ideally in a world where all players move confidentally and surely, there are a myriad of issues that plague the consistency of this model. 

If a player begins to disconnect one or more Blinks and accidentally disconnects the fractured bunch, upon reconnecting the fractured Blinks, the game-state between the Blinks will be disrupted and it will be impossible to 'sync' the gamestates of the Blinks back together without resetting the entire game. (ex. one Blink will read that it is player 1's turn and emit a blue light, while the rest emit a red light). 

In the dev kit versions of Blinks, the Blinks are extremely sensitive to errant line or touches that interfere with the infrared signal. Any errant interference will disrupt the game state as well, resulting in a irrecoverable, inconsistent game state. However, these issues can most likely be remedied once future versions of Blinks have rubber tops. 
