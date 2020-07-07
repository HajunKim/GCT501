Final_Report for GCT501  
===================
The new way of designing with Music  
------------
Hajun Kim, Jaekwon Lim, Conor O’Malley

<img src="https://user-images.githubusercontent.com/37058246/86720950-7aed8000-c060-11ea-921b-9ddee04c3e1d.png" width=60% height=60%>

## Contents

### 1. Summary

##### 1) Concept
##### 2) Software
##### 3) Hardware

### 2. Process

##### 1) Development 
##### 2) Fabrication 
##### 3) Presentation 

### 3. Role of members  

------------------------------------------------------------------

### 1. Summary 


#### 1) Concept
The MoMu consists of 2 technical concepts:
a <strong>digital instrument</strong> that users can move to create music with, and a <strong>digital platform</strong> that allows others to collaborate and share with the music they have created.

###### Instruments
The Instrument consists of Accelerometer sensors that transform the user’s movements into digital drum beats and custom synthesizer sounds. This instrument was designed to combine the creative freedom of playing an instrument and the interpretive movement of dance without the limitations of either. 

<img src="https://user-images.githubusercontent.com/37058246/86722470-df5d0f00-c061-11ea-88c1-2b975177fe67.png" width=30% height=30%>

###### Platform
The MoMu Platform is a digital space where users can share and collaborate with other artists. Users upload their work and artwork to the digital social media platform, and others can view, enjoy and remix their work. This organic community flow allows for the users to seek out unique sounds and dance moves that can inspire and encourage more creative music and rhythm. 

<img src="https://user-images.githubusercontent.com/37058246/86719529-1d0c6880-c05f-11ea-8da1-72a726fca923.jpeg" width=30% height=30%>

------------------------------------------------------------------

#### 2) Software

#### Programming Language

<img src="https://user-images.githubusercontent.com/37058246/86724476-c9504e00-c063-11ea-9f2d-14ce9caa7c8d.png" width=30% height=30%>

###### python
We used Python to control the main process and process for the accelerometer sensor. There were three main reasons for using Python. First, it is easy to modularize the program. Second, Libraries for communicating or playing sounds are well implemented. Finally, It is the most used programming language in raspberry pi.

<img src="https://user-images.githubusercontent.com/37058246/86724488-ca817b00-c063-11ea-8479-2f6879de23ac.png" width=15% height=15%>

###### Go
We used Go language to control the parameters that we can get by utilizing leap motion. We can synchronizes leap motion directly by using Go language. Go language has great module called Go bot and It has functions that adjust the coordinates perceived by leap motion to value appropriately.


#### Module


###### Socket
We used socket communication to communicate with raspberry pi which is used for accelerometer sensor. There are many ways to communicate with Raspberry Pie, but in our project it was important to communicate quickly in real time, so we used the simplest method.

###### Pygame
In our project, it was important to play musical instruments according to the input that occurred in real time. We used pygame for this purpose. Pygame does not wait until the sound is finished after playing the sound and, but performs the code immediately on the next line. It was convenient to use because there was no need for additional thread coding.
Sklearn - Sklearn is a machine learning library for python. User motion was indistinguishable by the raw data of the accelerometer sensor. We solved this problem by using unsupervised learning.

###### Go Bot
Go bot is a strong library that requires very simple setting to be used. The module provides the functions to control nearly 30 devices including leap motion. It offers simple structure code and it helps the user get as sense quickly. In particular, regarding Leap Motion, it provided functions related to various hand movements, but it was less accurate than expected, so we had to make the necessary actions by tuning the coordinate value parameters. 

------------------------------------------------------------------

#### 2) Hardware

###### RasPi & Accelerometer
We chose raspberry pie as a small computer to process the value of the accelerometer sensor and send it to the main process. we used mpu6050 as a sensor for motion of the user.

<img src="https://user-images.githubusercontent.com/37058246/86719625-357c8300-c05f-11ea-8070-ae5512f8fbf0.jpeg" width=15% height=15%>

###### Leap Motion
eap Motion is a strong device that can senses human hand motion accurately in real time. Therefore it can deal with 3 dimensional interactions such as requiring x,y,z coordinates. It is being used in various prototype types around the world, provided with sufficient modules in various languages. However, due to frequent updates, most modules do not operate properly. It shows excellent performance against price, and not only tracks the coordinates of the hand, but also has the potential to implement various hand movements and forms as a function. However, leap motion tracking scope is limited due to its method, based on infrared cameras located at the top of the device. it is possible to trace up to 15 cm each directions(Front, Back, Right, Left).

<img src="https://user-images.githubusercontent.com/37058246/86728028-fc481100-c066-11ea-80dc-0bafb65577fa.png" width=15% height=15%>

###### 3D Printing 
Two specific wearable 3D Designs needed to be designed for the user. One was for specifically the accelerometer to limit movement on the body as the sensor could be very sensitive. This was designed as a Wristband and fitted for the sensors pins and mounting bracket. Second, the Raspberry Pi and mobile Battery Bank needed to be secured to the user in an unobtrusive way. This was designed first as a waistband mount, but was later changed to an Armband strap to reduce jumper cable length.

------------------------------------------------------------------

### 2. Process 

#### 1) Development
Development was led by JaeKwon. HaJun was in charge of detecting motion by using leapmotion.

#### main process 
In the main process, it is repeated to receive the values of the leap motion and the accelerator sensor. The values received would be processed through the controller. 
1. In the controller, the object for playing musical instruments is initiated.
2. In this object, there are functions for playing musical instruments depending on index and changing the internal variable for the effects including reverberation and distortion. 
3. The controller uses this object after deciding what to do by received data. 
4-1. By received data from accelerometer sensor and leap motion, it decides to play musical instruments. 
4-2. By received data from leap motion, it decides to change the parameters for reverberation and distortion which is in the object for playing instruments.

###### Leapmotion 
The module, Gobot, offers diverse hand gesture functions that returns active value when the action is taken. However, due to the frequent update for the software of leap motion, it was not able to use those. <strong>We had to build up our own motion returns certain value.</strong> Since we wanted to make a special effect sound through leap motion, 3 respective motions mapping to each sounds was organized. It should have been very simple and easily understood to people, while at the same time showing the potential to be used in various ways depending on their preferences in the future. We conducted an experiment to see how the coordinates would be seen when the leap motion is being used.
Based on these values, three actions were constructed. While the x and z values were fixed, only the y values were changed to make the sound of special effects(figure 1), and the x and z values were changed respectively to change the effects of sound to reverb and distortion. (figure 2,3)



acc sensor
send
To process the value of accelerometer sensor, unsupervised learning model was used. we train it ourselves. We made the dataset for the model by doing two types of motion with wearing the accelerometer sensor. This training model does the classification of motion.
receive
When program receives the data from accelerometer sensor, it returns the sound index. If it returns all the value right after return the motion value, then it makes a problem which plays the instrument sounds several times for one motion. To solve this problem, it is developed to ignore the 5 values right after sensing the motion. The number of ignored value can be different depending on calibration.
connection with leap motion // For HAJUN

connection with accelerometer sensor
we used socket connection for sending the value of accelerometer sensor. Received part was developed to check the connection first before receiving the data continuously.

2. Fabrication  - 3D Print designs and fabrication was led by Conor. All 3D Prints were printed from Professor Ahn’s Ultimaker3 3D Printer. 
The 3D print components were first designed in Blender and Meshmixer, Sliced in Cura and printed with flexible TPU Filament, which matched specifications for wearable devices. The supports were created with Breakaway Filament, allowing for fast removal when paired with the flexible TPU. 
The Wristband module was designed as one continuous piece that allowed for snapping in place. 
The Armband was designed as three separate pieces, and used M3 screws to hold the two ends of the armbands to the center Pi Console. Then the Armband straps locked in place used snapback plastic design.


3. Presentation - Presentation Slides and Organization was led by HaJun.
The slides were first organized and a rough outline of the script was delegated across the team. 
Next, the slides were designed and decorated while team members wrote their specific scripts to match presentation objectives. 
Afterwards, slides were polished, combined and edited for continuity.
Finally, the presentation was practiced as a team to match the format of the presentation when possible.

------------------------------------------------------------------

### 3. Role of Members 

//Describe what and how each member did.

HaJun // For HAJUN
JaeKwon - Development
JaeKwon was in charge of development of the main process and connecting with the accelerometer sensor.
Conor - Digital Fabrication / 3D Printing
Conor designed and 3D printed the accelerometer sensor bracelet and the Raspberry Pi/Battery Bank Armband

