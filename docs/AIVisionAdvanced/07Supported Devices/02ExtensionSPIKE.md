# Supported Devices
## Introduction
<!-- 这是一张图片，ocr 内容为： -->
![](img/SP01.png)

The LEGO SPIKE Prime AI and robotics programming learning series is based on the SPIKE Prime Hub system.

The kit consists of the SPIKE Prime hub, motors, sensors, actuators, and LEGO Technic structural parts.

This document focuses on integrating the vision module with the SPIKE Prime controller.

## Quick Start
Since SPIKE Prime does not allow the addition of custom modules, the vision module simulates a SPIKE color sensor in order to work with SPIKE Prime.

Before use, set the module's port protocol to SPIKE mode.

(Refer to the UI Interface section for operation details. For further details, see SPIKE Compatibility Mode.)

### Hardware Preparation
| <!-- 这是一张图片，ocr 内容为： -->
![](img/SP02.png) | <!-- 这是一张图片，ocr 内容为： -->
![](img/SP03.png) |
| :---: | :---: |
| SPIKE Prime Hub | K210 AI Vision Sensor |
| <!-- 这是一张图片，ocr 内容为： -->
![](img/SP04.png) | <!-- 这是一张图片，ocr 内容为： -->
![](img/SP05.png) |
| Adapter Board | Grove male-to-male cable |
![](img/SP06.png) | <!-- 这是一张图片，ocr 内容为： -->
![](img/SP07.png) |
| Dual-head WeDo 2.0 cable | SPIKE Motor |


### Software Preparation
You can enter the [LEGO SPIKE](https://spike.legoeducation.com/) programming page to program the SPIKE Prime Hub. 

1. Go to the LEGO SPIKE webpage.
2. At the bottom right, click SPIKE Prime Essential/Prime Set.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP08.png)

3. Click New Project.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP09.png)



4. Select a programming method you are familiar with. (The following introduces WORD MODULE programming.)

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP10.png)



5. Enter the block WORD MODULE interface.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP11.png)



6. Click Show Block Extensions.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP12.png)



7. Select More Sensor Blocks.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP13.png)



8. In the More Sensor Blocks section, an additional block named Get Color Sensor RGB Value will appear.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP14.png)

### Usage Example
Connect the vision module to Port A of the SPIKE hub and manually switch it to Tag Recognition Mode.

If no tag is detected, the SPIKE matrix display shows N.

If a tag is detected, the SPIKE matrix display shows the Tag ID.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP15.png)

Demonstration:

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP16.gif)



## Usage Instructions  
Since the vision module emulates a color sensor, it is read-only. This means that you can only use the built-in color sensor blocks in SPIKE to read values from the vision module. Mode switching must be done manually on the vision module itself.

The output values of the vision module in different modes correspond directly to the values of the SPIKE color sensor. For detailed mapping, please refer to the SPIKE Compatibility Mode section.



After completing the above steps, connect the vision module to the SPIKE Prime hub. The hub will detect the module as a color sensor, as shown in the figure below:

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP101.png)

### Color Recognition
1. Switch the vision module to Color Recognition Mode.
2. Read the R value of the detected color from the vision module and display it on the SPIKE Prime hub.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP15.png)



### Color Block Tracking
1. Switch the vision module to Color Block Tracking Mode.
2. If a color block is detected, the x-coordinate of the block will be displayed on the SPIKE Prime hub; otherwise, N will be shown.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP23.png)


### Tag Recognition
1. Switch the vision module to Tag Recognition Mode.
2. If a tag is detected, the Tag ID will be displayed on the SPIKE Prime hub; otherwise, N will be shown.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP24.png)



### Line Recognition
1. Switch the vision module to Line Recognition Mode.
2. If a line is detected, the X-coordinate of the line will be displayed on the SPIKE Prime hub; otherwise, N will be shown.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP25.png)



### 20-Class Object Recognition
1. Switch the vision module to 20-Class Object Recognition Mode.
2. If an object is detected, its ID will be displayed on the SPIKE Prime hub; otherwise, N will be shown.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP26.png)



### QR Code Recognition
1. Switch the vision module to QR Code Recognition Mode.
2. If a QR code is detected, its X coordinate will be displayed on the SPIKE Prime hub; otherwise, N will be shown.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP27.png)



### Face Attribute Recognition
1. Switch the vision module to Face Attribute Recognition Mode.
2. If no face is detected, the SPIKE Prime hub will display N.
3. If a face is detected: Open mouth → `o` Closed mouth → `-`

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP28.png)



### Face Recognition
1. Switch the vision module to Face Recognition Mode.
2. Manually control the module to learn faces.
3. If no learned face is recognized, the SPIKE Prime hub will display N.
4. If a learned face is recognized, the hub will display the X-coordinate of the detected face.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP29.png)



### Deep Learning
1. Switch the vision module to Deep Learning Mode.
2. Manually control the module to perform deep learning training.
3. If no object is recognized, the SPIKE Prime hub will display N.
4. If an object is recognized, the hub will display the corresponding ID.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP30.png)



### Road Sign Recognition
1. Switch the vision module to Road Sign Recognition Mode.
2. If no road sign is recognized, the SPIKE Prime hub will display N.
3. If a road sign is recognized, the hub will display the corresponding road sign ID.

<!-- 这是一张图片，ocr 内容为： -->
![](img/SP31.png)















