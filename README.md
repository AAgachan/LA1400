# LA1400
```java
package AtputharasaAgach;
import robocode.*;


public class Zeus extends JuniorRobot {

  int moveCounter = 0;
  int moveDirection = 1;
  int moveDistance = 100;

  public void run() {
    setColors(black, black, black);

    while (true) {

      if (others > 25) { // Checks if opponents are higher than 25
        playSafe(); // defensive playstyle
      } 
      else if (others < 25) {
        playNeutral();  //balanced playstyle
      } 
      else if (others < 15) {
        playAggresive();  //offensive playstyle
      }
    }
  }

  public void onScannedRobot() {
    fire(2);
    turnRight(250);
    ahead(450);
    if(scannedDistance >= 1650){ // check if the scanned distance is greater than or equal to 1650 units
      fire(3);
    } else { 
      bearGunTo(scannedBearing);  // turn the gun to face the scanned robot
      fire(2);
      ahead(scannedDistance + 15); // move ahead by the scanned distance + 15 units
      turnRight(scannedBearing);
      fire(4);
    }
}
  public void onHitByBullet() {  
      turnLeft(90);
      ahead(fieldHeight / 2);  // move ahead by half the height of the field
    }

  public void onHitWall() {
      back(fieldHeight / 4);  // move back by a quarter of the height of the field
      turnLeft(90);
    }
  


public void playSafe() { // Method to play safely
  if (heading < 90) { // Check heading relative to the North direction
    back((int) robotY); // Move back by the robot's Y position
    turnLeft(heading - 90); // Turn left to face North
  } else if (heading > 90) {
    ahead((int) robotY); // Move ahead by the robot's Y position
    turnRight(90 - heading); // Turn right to face North
  } else {
    back((int) robotY); // Move back by the robot's Y position
  }
  frugalEnergy();
}


public void playNeutral() { // Method to play neutral
  if (moveCounter % 20 == 0) { // Check if 20 moves have passed
      moveDirection *= -1; // Change the direction of movement
  }
  ahead(moveDistance * moveDirection);  // Move by the distance and direction determined
  turnLeft(90);
  moveCounter++;
  frugalEnergy();   // Call the frugalEnergy method
  moveDistance += 5;
}

public void playAggresive() { // Method to play aggresivly
  if (scannedDistance > 0) { // Check if a robot was scanned
    int angle = scannedBearing + heading - gunHeading; // Calculate the angle to turn the gun to face the scanned robot
    bearGunTo(angle);
    back(scannedDistance - 50);
    turnLeft(scannedBearing);
  } else {
    turnGunLeft(360);
    back(fieldHeight / 2);     // Move back by half the height of the field
  }
  frugalEnergy(); // Call the frugalEnergy method
}

public void frugalEnergy() {
  if (energy < 20) { // Check if energy is less than 20
    ahead(fieldHeight / 2); // Move ahead by half the height of the field
    turnLeft(180);
    back(fieldHeight / 4); // Move back by a quarter of the height of the field
    turnLeft(90);
  }
}
}
```
