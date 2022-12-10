ECE 16 Design Challenge

Jeremy Wong, Syed Islam

A16994954, A16798921

# Design Challenge

### Helpful Links:
> [Final Project Challenges](https://docs.google.com/document/d/1L3A4bCqKNH0l9c5Sk9MfJYCXA3jDJcp1VEj8NRmvWfM/edit#)

> [Final Project Submission Structure](https://docs.google.com/document/d/16jEhmbwYTFgKXTMDjRFHbVoV7-BgzolrVEYCSBPkv8I/edit)

> [OpenCV Facial Recognition](https://realpython.com/face-recognition-with-python/)

> [Face Recognition Library](https://face-recognition.readthedocs.io/en/latest/index.html) (used heavily in project)

> [ESP32 Communication Using ESP-NOW Protocol](https://randomnerdtutorials.com/esp-now-two-way-communication-esp32/)

> [Serial Communication Between Two ESP32s](https://stackoverflow.com/questions/49212371/serial-communication-between-two-esp32)

> [Using Servo Motors with ESP32](https://dronebotworkshop.com/esp32-servo/#:~:text=The%20ESP32%20has%20analog%20outputs,in%20WiFi%20and%20Bluetooth%20capabilities.)


[Design Challenge YouTube Video](https://youtu.be/vI20D-6ep7s)

## Discussion of Finding the Need
1. What is the use case you are trying to address?
>> The use cases we are trying to address are related to convenience with unlocking and opening one's front door: when one forgets their house keys, when one cannot open the door for theirself for medical reasons or because their hands are full, and when one cannot open the door for a guest because they are busy. 
2. Why is this problem worth addressing?
>> This problem is worth addressing because in 2012, over 2 million people were locked out of their homes in New York<sup>[1]</sup>, trying to balance groceries or packages in one hand while fetching for one's keys is an extremely common issue, and working from home is becoming more and more prevalent which keeps people tied to their computers and prevents them from being able to let people into the house.
3. Who is/are the intended user(s)?
>> The intended users are homeowners or anyone who can install this system in their living arrangements. Since this door system requires a motor-controlled door and a security camera, this is not as feasible of an option for people who live in apartments and condominiums.
4. How is your solution addressing the needs of the user?
>> Our solution is addressing the needs of the user by providing a keyless method of entry into one's home, which eliminates the possibility of forgetting one's keys in the first place. Our solution also provides a touchless system that only requires one's exposed face to enter rather than having to physically open the door theirself. Lastly, our solution provides a way to remotely open the door for guests or open automatically for trusted visitors.

[[1] THE END OF HOUSE KEYS: The August Smart Lock Wants To Make It So You'll Never Get Locked Out Of Your Home Again](https://www.businessinsider.com/august-smart-lock-ceo-interview-2013-10)

## Discussion of Our Solution Design
1. What did you choose?
>> We chose to create a security camera-controlled door system that automatically opens for people whose faces are registered in the system, and can also be opened using a remote control that is operated by the homeowner. The remote control can open the door from a distance, add new faces into the computer system to be recognized in the future, and toggle the face detection system on and off. 
2. Why did you choose it?
>> We chose this solution design because we thought it would be an interesting way to use current face detection technology to create a system that is affordable, relatively simple, and can be used by a large percentage of the population. We also chose this solution design because we wanted to make a system using two ESP32s in communication with one another (though we ended up using the computer as the middleman between the two MCUs to simplify the design). 
3. What was your thought process in the design?
>> Our thought process initially involved the simple idea of using OpenCV to open the door automatically, and as we progressed through the project, we gradually added more and more complexity to the system. We realized that using only face detection to open the door was not the only functionality that could be included with a smart door, so we also opted to design a remote control for the door as well. Originally the remote only had one button, which was used to open the door, but after consulting the TAs, we came to the conclusion that that would also not be complex or comprehensive enough, so we added two more buttons with two more functions for the remote control.
