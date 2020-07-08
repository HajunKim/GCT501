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

<img src="https://user-images.githubusercontent.com/37058246/86870469-6918e500-c113-11ea-9e00-46b22bcb03cf.jpg" width=30% height=30%>

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

<img src="https://user-images.githubusercontent.com/37058246/86719625-357c8300-c05f-11ea-8070-ae5512f8fbf0.jpeg" width=30% height=10%>

###### Leap Motion
Leap Motion is a strong device that can senses human hand motion accurately in real time. Therefore it can deal with 3 dimensional interactions such as requiring x,y,z coordinates. It is being used in various prototype types around the world, provided with sufficient modules in various languages. However, due to frequent updates, most modules do not operate properly. It shows excellent performance against price, and not only tracks the coordinates of the hand, but also has the potential to implement various hand movements and forms as a function. However, leap motion tracking scope is limited due to its method, based on infrared cameras located at the top of the device. it is possible to trace up to 15 cm each directions(Front, Back, Right, Left).

<img src="https://user-images.githubusercontent.com/37058246/86728028-fc481100-c066-11ea-80dc-0bafb65577fa.png" width=30% height=30%>

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

4. By received data from accelerometer sensor and leap motion, it decides to play musical instruments. 

5. By received data from leap motion, it decides to change the parameters for reverberation and distortion which is in the object for playing instruments.

```python3

       class controller:
    def __init__(self):
        self.leapmotion = leapMotionSensor.leapMotionSensor()
        self.play_sound = playSound.playSound()
        self.acc = accSensor.accSensor()


    def processLeapMotinoData(self, received_data):
        if received_data == 3:
            self.play_sound.playTheSynthSound()
        elif received_data == 2:
            self.play_sound.changeTheReverbActivated()
        elif received_data == 1:
            self.play_sound.changeTheDistortedActivated()

    def processAccData(self,received_data):
        if received_data != -1:
            self.play_sound.playTheSound(received_data)

    def mainProcess(self):
        while True:
            receive_from_leap = self.leapmotion.receiveData()
            receive_from_acc = self.acc.receiveData()
            self.processLeapMotinoData(receive_from_leap)
            self.processAccData(receive_from_acc)

```

###### Leapmotion 
The module, Gobot, offers diverse hand gesture functions that returns active value when the action is taken. However, due to the frequent update for the software of leap motion, it was not able to use those. <strong>We had to build up our own motion returns certain value.</strong> Since we wanted to make a special effect sound through leap motion, 3 respective motions mapping to each sounds was organized. It should have been very simple and easily understood to people, while at the same time showing the potential to be used in various ways depending on their preferences in the future. 

1. We conducted an experiment to see how the coordinates would be seen when the leap motion is being used.

2. Based on these values, three actions were constructed. 

3. While the x and z values were fixed, only the y values were changed to make the sound of special effects(figure 1)

4. the x and z values were changed respectively to change the effects of sound to reverb and distortion. (figure 2,3)

```GO
 l.On(leap.HandEvent, func(data interface{}) {
                        //almPosition = data.(leap.Hand).StabilizedPalmPosition
                        PalmPosition = data.(leap.Hand).PalmPosition
                        //fmt.Println(leap.Hand)
                        //TelloQE.Store(data.((leap.Hand).R[0][0]-0.5)*10)//rotate
                        if data.(leap.Hand).S < 1 {
                                if PalmPosition[0] < -50{
                                        PalmPosition[0]=-50}
                                if PalmPosition[0] > 50{
                                        PalmPosition[0]=50}
                                PalmPosition[1] = PalmPosition[1]-150
                                if PalmPosition[1] < -50{
                                        PalmPosition[1]=-50}
                                if PalmPosition[1] > 50{
                                        PalmPosition[1]=50}
                                if PalmPosition[2] < -50{
                                        PalmPosition[2]=-50}
                                if PalmPosition[2] > 50{
                                        PalmPosition[2]=50}
                                TelloAD.Store(PalmPosition[0]) //left right/*/10*/
                                TelloJK.Store(PalmPosition[1])//up down/*/12-15*/
                                TelloWS.Store(-(PalmPosition[2]))// forward backward  */8)*/
                                /* rotation qe*/
                        }
                })
```
```python3

import csv

class leapMotionSensor:
    def __init__(self):
        print("leapMotionSenson object init")
        self.prev_received_Data_from_leap = -1
        self.thresholdIgnoreError = 1
        self.isError = 0
        self.blockTheSignal = 0
        self.blockNumber = 10

    def receiveData(self):
        lst = [0, 0, 0, 0]
        with open('test.csv', 'r') as file:
            reader = csv.reader(file)
            for row, x in enumerate(reader):
                if row > 3 or row < 0:
                    row = 3
                lst[row] = int(float(x[0]))
        result = -1
        if (lst[0] == 0 and lst[1] == 0 and lst[2] == 0):
            result = -1
        elif (lst[0] < -40 and (-40 < lst[1] < 40) and (-40 < lst[2] < 40)):
            result = 1
        elif (lst[1] < -40 and (-40 < lst[0] < 40) and (-40 < lst[2] < 40)):
            result = 2
        elif (lst[2] < -40 and (-40 < lst[1] < 40) and (-40 < lst[0] < 40)):
            result = 3

        resultInt = int(result)

        print("the leap motion value is", resultInt)

        if self.blockTheSignal > 0:
            self.blockTheSignal -= 1
            return -1
        else:
            if resultInt != -1:
                self.blockTheSignal = self.blockNumber

        return resultInt
```
###### acc sensor
send
To process the value of accelerometer sensor, unsupervised learning model was used. we train it ourselves. We made the dataset for the model by doing two types of motion with wearing the accelerometer sensor. This training model does the classification of motion. (figure 4,5)

receive
When program receives the data from accelerometer sensor, it returns the sound index. If it returns all the value right after return the motion value, then it makes a problem which plays the instrument sounds several times for one motion. To solve this problem, it is developed to ignore the 5 values right after sensing the motion. The number of ignored value can be different depending on calibration.


```python3

       def receiveData(self):  # return -1: no acc motion , 0 : verticalMotion , 1: horizontalMotion , 2: circleMotion
        # 1 stop - 1, 0 motion 0 , 3 motion 1 , 2 motion 2
        receive = self.clientSock.recv(1024)[0]
        print("receiveAccSensor : ", receive)
        if (receive % 2) == 1:
            receive = receive - 2
        if receive == 2:
            receive = 0

        if self.blockTheSignal > 0:
            self.blockTheSignal -= 1
            return -1
        else:
            if receive != -1:
                self.blockTheSignal = self.blockNumber

        return receive

```


###### connection with leap motion
We used csv file for sending certain motion value from GO language to python, Go language writes down the value in every 0.001 seconds and python read it by while statement. The implementation was seem working in real time.
```GO


	rows := [][]string{

	{strconv.FormatFloat(s.ws,'f',5,64)},
	{strconv.FormatFloat(s.ad,'f',5,64)},
	{strconv.FormatFloat(s.jk,'f',5,64)},
	{strconv.FormatFloat(s.sense,'f',5,64)},
	}
 
       gobot.Every(5*time.Millisecond, func() {

	csvfile, err := os.Create("test.csv")
 
	if err != nil {
		log.Fatalf("failed creating file: %s", err)
	}
 
	csvwriter := csv.NewWriter(csvfile)
 
	for _, row := range rows {
		_ = csvwriter.Write(row)
	}
 
	csvwriter.Flush()
 
        csvfile.Close()
	}
```
###### connection with accelerometer sensor
we used socket connection for sending the value of accelerometer sensor. Received part was developed to check the connection first before receiving the data continuously.

```python3

      self.ip = '192.168.1.248'
      self.port = 8080
      self.clientSock = socket(AF_INET, SOCK_STREAM)
      self.clientSock.connect((self.ip, self.port))
      print('연결 확인 됐습니다.')
      self.clientSock.send('I am a client'.encode('utf-8'))
      print('메시지를 전송했습니다.')
      data = self.clientSock.recv(1024)
      print('받은 데이터 : ', data.decode('utf-8'))

      self.blockTheSignal = 0
      self.blockNumber = 5

```


#### 2. Fabrication  - 3D Print designs and fabrication was led by Conor. All 3D Prints were printed from Professor Ahn’s Ultimaker3 3D Printer. 
The 3D print components were first designed in Blender and Meshmixer, Sliced in Cura and printed with flexible TPU Filament, which matched specifications for wearable devices. The supports were created with Breakaway Filament, allowing for fast removal when paired with the flexible TPU. 
The Wristband module was designed as one continuous piece that allowed for snapping in place. 
The Armband was designed as three separate pieces, and used M3 screws to hold the two ends of the armbands to the center Pi Console. Then the Armband straps locked in place used snapback plastic design.


<img src="https://user-images.githubusercontent.com/37058246/86719715-49c08000-c05f-11ea-8909-19cee48fcc7b.png" width=30% height=30%>


#### 3. Presentation - Presentation Slides and Organization was led by HaJun.
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

