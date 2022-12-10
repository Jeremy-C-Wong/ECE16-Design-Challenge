ECE 16 Final Project

Jeremy Wong, Syed Islam

A16994954, A16798921

# Final Project

### Helpful Links:
> [Final Project Challenges](https://docs.google.com/document/d/1L3A4bCqKNH0l9c5Sk9MfJYCXA3jDJcp1VEj8NRmvWfM/edit#)

> [Final Project Submission Structure](https://docs.google.com/document/d/16jEhmbwYTFgKXTMDjRFHbVoV7-BgzolrVEYCSBPkv8I/edit)

> [OpenCV Facial Recognition](https://realpython.com/face-recognition-with-python/)

> [Face Recognition Library](https://face-recognition.readthedocs.io/en/latest/index.html) (used heavily in project)

> [ESP32 Communication Using ESP-NOW Protocol](https://randomnerdtutorials.com/esp-now-two-way-communication-esp32/)

> [Serial Communication Between Two ESP32s](https://stackoverflow.com/questions/49212371/serial-communication-between-two-esp32)

> [Using Servo Motors with ESP32](https://dronebotworkshop.com/esp32-servo/#:~:text=The%20ESP32%20has%20analog%20outputs,in%20WiFi%20and%20Bluetooth%20capabilities.)

## Table of Contents
1. Grand Challenge - Part 1: Space Invaders Controller
2. Grand Challenge - Part 2: Design Challenge

## Grand Challenge - Part 1: Space Invaders Controller

[Space Invaders YouTube Video](https://youtu.be/bdRmeYbIzVg)

### Improvements

#### Stabilized Controller Tilt
> We utilized the starter code and transferred the logic from Arduino to Python, using the Arduino to send the accelerometer data to Python where the processing took place. The logic remained mostly the same, but instead of using a value of 0 to determine whether the controller was tilted left, right, up, or down, we increased or decreased the values to make the controller less sensitive to slight deviations from the resting state, using especially high values for up and down in order to prevent the player from unintentionally adjusting the sensitivity (see *Improved Sensitivity (Adjustable)*).

#### Decoupled Movement and Shooting
> We used a push button for shooting to create a more conventional controller interface, which allowed us to easily decouple the movement from the shooting. Upon pressing the push button, the ESP32 sends the message "FIRE" to Python, which then receives it and sends the command "FIRE" to the socket server. This process happens in an if-statement, with the movement in an else-clause, which technically means that the movement and shooting are not decoupled, but because the data is received in high volumes, the timing difference is negligible, making the two actions effectively decoupled.

#### Improved Sensitivity (Adjustable)
> We used the tilting of the controller along the y-axis to adjust the sensitivity (or effectively the movement speed) to allow different players with different preferences to play the game. Tilting up the controller increases the sensitivity by decreasing the cooldown between each message sent to the socket server, while tilting down the controller does the opposite.

### Features

#### Added OLED to Display Score and Lives
> We added the OLED to that displays the current score and lives of the player. In Python, the socket server sends the encoded score and life data to the client which receives the data, decodes it, then sends that data to the ESP32. The ESP32 then parses the data into two strings, one with the score and one with the lives, then displays that data on the OLED.

#### Added Buzzer Motor to Indicate Losing a Life
> We added a buzzer motor that activates for one second after losing a life. Using the same process as above to send the data to the ESP32, we activated the motor each time the number of lives changed, or more precisely, when the state changed. The state was determined by each time the motor had to be deactivated, which only happened each time the lives had changed.

#### Added Quit Button
> We utilized a second push button to quit the game. Upon pressing the button, the ESP32 sends the message "QUIT" to the Python serial buffer which then receives it and raises a KeyboardInterrupt, ending the program.

### Controller Instructions

1. Tilt left or right to move left or right, respectively.
2. Tilt the front of the controller up to increase the sensitivity; tilt down to decrease the sensitivity.
3. Press or hold the left button to shoot.
4. Press the right button to quit the game (after the game has started).

## Grand Challenge - Part 2: Design Challenge

[Design Challenge YouTube Video](https://youtu.be/vI20D-6ep7s)

### Discussion of Finding the Need
1. What is the use case you are trying to address?
>> The use cases we are trying to address are related to convenience with unlocking and opening one's front door: when one forgets their house keys, when one cannot open the door for theirself for medical reasons or because their hands are full, and when one cannot open the door for a guest because they are busy. 
2. Why is this problem worth addressing?
>> This problem is worth addressing because in 2012, over 2 million people were locked out of their homes in New York<sup>[1]</sup>, trying to balance groceries or packages in one hand while fetching for one's keys is an extremely common issue, and working from home is becoming more and more prevalent which keeps people tied to their computers and prevents them from being able to let people into the house.
3. Who is/are the intended user(s)?
>> The intended users are homeowners or anyone who can install this system in their living arrangements. Since this door system requires a motor-controlled door and a security camera, this is not as feasible of an option for people who live in apartments and condominiums.
4. How is your solution addressing the needs of the user?
>> Our solution is addressing the needs of the user by providing a keyless method of entry into one's home, which eliminates the possibility of forgetting one's keys in the first place. Our solution also provides a touchless system that only requires one's exposed face to enter rather than having to physically open the door theirself. Lastly, our solution provides a way to remotely open the door for guests or open automatically for trusted visitors.

[[1] THE END OF HOUSE KEYS: The August Smart Lock Wants To Make It So You'll Never Get Locked Out Of Your Home Again](https://www.businessinsider.com/august-smart-lock-ceo-interview-2013-10)

### Discussion of Our Solution Design
1. What did you choose?
>> We chose to create a security camera-controlled door system that automatically opens for people whose faces are registered in the system, and can also be opened using a remote control that is operated by the homeowner. The remote control can open the door from a distance, add new faces into the computer system to be recognized in the future, and toggle the face detection system on and off. 
2. Why did you choose it?
>> We chose this solution design because we thought it would be an interesting way to use current face detection technology to create a system that is affordable, relatively simple, and can be used by a large percentage of the population. We also chose this solution design because we wanted to make a system using two ESP32s in communication with one another (though we ended up using the computer as the middleman between the two MCUs to simplify the design). 
3. What was your thought process in the design?
>> Our thought process initially involved the simple idea of using OpenCV to open the door automatically, and as we progressed through the project, we gradually added more and more complexity to the system. We realized that using only face detection to open the door was not the only functionality that could be included with a smart door, so we also opted to design a remote control for the door as well. Originally the remote only had one button, which was used to open the door, but after consulting the TAs, we came to the conclusion that that would also not be complex or comprehensive enough, so we added two more buttons with two more functions for the remote control.

## Division of Labor

For the Space Invaders Challenge, we split the labor by having one person (Jeremy) handle the improvements for the controller, and the other (Syed) handle the features. I did most of my work on the *space_invaders_controller.py* file, while Syed worked primarily on the *SpaceInvadersController.ino* file, and then we integrated our work together to produce the final product.

For the Design Challenge, we split the labor by having one person (Jeremy) handle the communication between the two ESP32s (or rather the ESP32 communication), the Arduino functionality, and some of the main Python program, while the other (Syed) handled more of the main program involving the face detection and a bit of the unlocking logic. Both of us worked together to add additional functionality such as the camera capture to save faces into the computer system, as well as the functionality to enable/disable the system. For the presentation and demonstration part, Syed did more of the talking and writing of the outline, but I also contributed some to that portion.
