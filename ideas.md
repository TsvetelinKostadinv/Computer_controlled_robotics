# Ideas for a project

## Camera-less motion tracking
Most solutions that track motion of hands, legs or even the whole body make use of a camera which consists of colour or gesture recognition. However we can speed up the process of capturing and transforming of the data, subsequently taking actions based on the data.

### Anticipated parts
- Microcontroller - be it Arduino or esp32, probably would need 2 - gatherer and actor
  - We need some form of computer in order to transform the data and output it to some transmitter
- Transmitter
  - Options include: Bluetooth, Wi-Fi, radio
  - Need to overlay our transmission protocol on top of an existing ones
  - Furthermore if it would be long distance, it could be UDP, but that is a design choice.
  - For the given project maybe local wi-fi communication would be best
- Sensors
  - We need something to gather the data.
  - Accelerometer for the speed, angle and angular momentum of a given part of the body.
  - Tensoresistors could measure the "straightness" of joints - essentially the opposite of muscles
- The "server" which will forward the received data to the body that will be moved according to the gathered gestures from the microcontroller
- Motors for the movement
  - Technically we can do whatever with the data, but my idea is some day equip the whole body with sensors and build a whole separate body that mimics the person wearing the set.
  - As a start we can measure just the hand(elbow and palm gestures and relative positions).

### Technologies
The possibilities are endless. C++🤖, Java♥ and C#🤮 would be easiest for the development of the "server" computer. For the embedded system there isn't as much freedom with tech stack, so there the choice is centered around the choice of board.

### Chain
```
Gatherer -> Server -> Actor
```
Probably would be the simplest chain
1. The gatherer
   - Measures from the sensors
   - Normalizes it
   - Serializes and transmits
1. The server
   - Receives the data from the gatherer
   - Checks for feedback from either side - gatherer or actor
   - Transforms it
   - Takes action according to the data - retransmits, handles gestures, etc.
1. The actor
   - Receives the data from the server
   - Acts according to the data - moves motors, displays info, etc.
   - Reports if there is error - moved into obstacle, battery low, etc.

## Swarm robotics
Heavier on the parts, but worth it in the end...

Implement simple rules for each robot and issue high level commands and let the lower level robots handle the rest. Maybe even go one step further and make 1 robot the boss and it will have more "weight" in taking decisions.

Here the minimal solution would be 3-4 small robots and 1 boss(cool idea to be a quadcopter which has more mobility)

Extra step would be to make them all drones, however, it would be more expensive and time-consuming so it would be a great long term project.
