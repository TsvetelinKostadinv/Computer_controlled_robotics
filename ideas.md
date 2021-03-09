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
  - Probably would need 1 for the elbow, 2 for the wrist(or some clever hack to get around it), and 5 for the digits for a total of 8 without the shoulder.

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
