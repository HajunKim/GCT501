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

<strong>Instruments</strong> 

The Instrument consists of Accelerometer sensors that transform the user’s movements into digital drum beats and custom synthesizer sounds. This instrument was designed to combine the creative freedom of playing an instrument and the interpretive movement of dance without the limitations of either. 

<img src="https://user-images.githubusercontent.com/37058246/86722470-df5d0f00-c061-11ea-88c1-2b975177fe67.png" width=30% height=30%>

<strong>Platform</strong> 

The MoMu Platform is a digital space where users can share and collaborate with other artists. Users upload their work and artwork to the digital social media platform, and others can view, enjoy and remix their work. This organic community flow allows for the users to seek out unique sounds and dance moves that can inspire and encourage more creative music and rhythm. 

<img src="https://user-images.githubusercontent.com/37058246/86719529-1d0c6880-c05f-11ea-8da1-72a726fca923.jpeg" width=30% height=30%>

------------------------------------------------------------------

#### 2) Software

#### Programming Language

<img src="https://user-images.githubusercontent.com/37058246/86724476-c9504e00-c063-11ea-9f2d-14ce9caa7c8d.png" width=30% height=30%>
<strong>python</strong>

We used Python to control the main process and process for the accelerometer sensor. There were three main reasons for using Python. First, it is easy to modularize the program. Second, Libraries for communicating or playing sounds are well implemented. Finally, It is the most used programming language in raspberry pi.

<img src="https://user-images.githubusercontent.com/37058246/86724488-ca817b00-c063-11ea-8479-2f6879de23ac.png" width=15% height=15%>
<strong>Go</strong>

We used Go language to control the parameters that we can get by utilizing leap motion. We can synchronizes leap motion directly by using Go language. Go language has great module called Go bot and It has functions that adjust the coordinates perceived by leap motion to value appropriately.


#### Module
###### python

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


