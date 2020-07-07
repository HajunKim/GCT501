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

#### 1) Software

##### Programming Language

<img src="https://user-images.githubusercontent.com/37058246/86724476-c9504e00-c063-11ea-9f2d-14ce9caa7c8d.png" width=30% height=30%>
<strong>python</strong>
We used Python to control the main process and process for the accelerometer sensor. There were three main reasons for using Python. First, it is easy to modularize the program. Second, Libraries for communicating or playing sounds are well implemented. Finally, It is the most used programming language in raspberry pi.

<img src="https://user-images.githubusercontent.com/37058246/86724488-ca817b00-c063-11ea-8479-2f6879de23ac.png" width=30% height=30%>
<strong>Go</strong>
We used Go language to control the parameters that we can get by utilizing leap motion. We can synchronizes leap motion directly by using Go language. Go language has great module called Go bot and It has functions that adjust the coordinates perceived by leap motion to value appropriately.

