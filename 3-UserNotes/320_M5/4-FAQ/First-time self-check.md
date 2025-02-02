# ***\*FQA for Robotic Arms-240301\****

## ***\*First-time self-check- Machine Joint Function Verification\****

**Attention:** When starting up the robotic arm, please ensure that it is not in a curled-up position or in a posture where joints are touching. It is recommended to start the robotic arm with the posture shown in the following diagram:

<div align=center> <img src="../../../resources/3-UserNotes/14-IssueFAQ/f1.jpg"> </div>
**The steps for joint control are as follows:**

#### **1.** ***\*Hardware Connection:\****

l For MyCobot 280 and Mech 270 series robotic arms, ensure that the power adapter and USB data cable are connected.

l For the mycobot320 series machines, please ensure that the power adapter, USB data cable, and emergency stop switch are connected. Make sure the emergency stop switch is in the released state. Failure to use the emergency stop switch correctly will result in the mycobot320 not functioning properly. Please refer to the diagram below for the emergency stop switch:

<div align=center> <img src="../../../resources/3-UserNotes/14-IssueFAQ/f2.jpg"> </div>

 

#### ***\*2.Software Environment Installation and Configuration:\****

l For M5 version robots, you need to install Python, the PyMyCobot library, and USB serial drivers. Please refer to the Python usage section in the Gitbook for specific instructions.

l For PI or JN version robots, there is no need to install and configure the usage environment separately. The factory provides pre-configured images in the robot system, which can be directly used for running robotic arm usage examples.

 

#### ***\*3.Select the Correct Communication Method:\****

Before using each communication method, ensure that the M5's LCD screen is set to the corresponding mode and remains in this communication state to control the robotic arm properly.

The M5 robotic arm has three communication methods: USB serial, WiFi, and Bluetooth communication. The most commonly used is the USB serial communication method.
<div align=center> <img src="../../../resources/3-UserNotes/14-IssueFAQ/f3.png"> </div>

**USB Serial Communication Method:**

l When using MyBlockly, Python, ROS, and other development methods, make sure the M5's LCD screen stays on the "Atom: ok" interface.

<div align=center> <img src="../../../resources/3-UserNotes/14-IssueFAQ/f4.png"> </div>


**WiFi Communication Mode:**

l When using TCP/IP examples in the Python section, make sure the M5's LCD screen remains in the WiFi communication interface.

<div align=center> <img src="../../../resources/3-UserNotes/14-IssueFAQ/f5.png"> </div>

**Bluetooth Communication Method:**

l When controlling with a mobile app, ensure that the M5's LCD screen stays in the Bluetooth communication interface.

<div align=center> <img src="../../../resources/3-UserNotes/14-IssueFAQ/f6.png"> </div>

#### ***\*4.Using USB Communication as an Example, Verify Joint Motion Python Source Code:\****

Note that using USB serial open mode requires selecting the corresponding serial port and baud rate to ensure normal communication between the robotic arm and the computer, thereby controlling the robotic arm normally.

Below is the corresponding information for the model, serial port, and baud rate:

| ***\*Common Problems and Solutions for Robotic Arms\**** | **Serial Port**                 | **Baud Rate** |
| -------------------------------------------------------- | ------------------------------- | ------------- |
| 260 M5                                                   | Win: COM*; Linux: /dev/ttyUSB*; | 115200        |
| 270 M5                                                   | Win: COM*; Linux: /dev/ttyUSB*; | 115200        |
| 280 M5                                                   | Win: COM*; Linux: /dev/ttyUSB*; | 115200        |
| 320 M5                                                   | Win: COM*; Linux: /dev/ttyUSB*; | 115200        |
| 260 PI                                                   | /dev/ttyAMA0                    | 1000000       |
| 270 PI                                                   | /dev/ttyAMA0                    | 1000000       |
| 280 PI                                                   | /dev/ttyAMA0                    | 1000000       |
| 320 PI                                                   | /dev/ttyAMA0                    | 115200        |
| 280 Jetson Nano                                          | /dev/ttyTHS1                    | 1000000       |

Note: When selecting the COM port for M5 series machines, it is necessary to choose based on the port number recognized by the current personal computer in real-time. This is because the COM port number recognized by each person's computer may vary and is not fixed. For specific selection methods, please refer to the answer to "Q: Why am I refused connection when selecting a certain COM port? Or, how do I find the corresponding COM port?" in this document.

**Robotic Arm Joint Motion MyBlockly Source Code:**

<div align=center> <img src="../../../resources/3-UserNotes/14-IssueFAQ/f7.png"> </div>

When you observe the effect of joint 1 of the robotic arm cyclically moving from 0 to 90 degrees three times, it indicates that joint 1 of the robotic arm responds normally. You can try changing the joint ID to test other joints and gradually learn to use other examples in GitBook or utilize the robotic arm for various interesting tasks!


It's worth mentioning that if you are not familiar with the code block development method of MyBlockly, there is a relatively quick way to verify joints: use the MyBlockly Quick Move Tool for simple joint motion control. For specific usage, please refer to the link below:

https://drive.google.com/file/d/1pDR-WBjkGrLcRdeshDmAMIWbEpu_jsJW/view?usp=sharing

<div align=center> <img src="../../../resources/3-UserNotes/14-IssueFAQ/f8.png"> </div>

**Robotic Arm Joint Motion Source Code:**

# The motion effect is the robotic arm revolving around the zero position, with joints 1-6 moving ±20 degrees one by one
```
import time
from pymycobot.mycobot import MyCobot

if __name__ == "__main__":
    cobot = MyCobot('com22', 115200)  # Choose the corresponding port and baud rate according to the model of the robot
    cobot.set_fresh_mode(1)
    cobot.send_angles([0, 0, 0, 0, 0, 0], 20)
    time.sleep(2)
    print("start")
    for i in range(1, 7):
        cobot.send_angle(i, -30, 20)
        time.sleep(2)
        cobot.send_angle(i, 30, 20)
        time.sleep(2)
        cobot.send_angle(i, 0, 20)
        time.sleep(2)
```


When you see the motion effect of the robotic arm revolving around the zero position, with joints 1-6 moving ±20 degrees, it indicates that joints 1-6 respond normally. You can gradually learn to use other examples in the Gitbook or use the robotic arm to do various interesting things!

If you don't see the corresponding effect when executing the example, please refer to the following common problem-solving solutions. Also, make sure you have checked the following 5 points before contacting technical support:

1. Is the robotic arm able to lock normally after power-on? If it cannot lock, please refer to the hardware-related issue: "Q: How to solve the problem of the robotic arm not locking after power-on?" for troubleshooting.
2. If you are using an M5 series robotic arm,is the computer connected to the USB port on the side of the M5stack via type-c?
3. If you are using an M5 series robotic arm,is the LCD screen currently staying on the "Atom: ok" interface?
4. If you are using a 320 series product, please ensure that your emergency stop switch is connected and in the released state.
5. Are there any error messages when running the code?

Please describe the details of your usage as much as possible, and if possible, provide an operation video, which will help to quickly analyze and locate the problem. Thank you in advance!

 
