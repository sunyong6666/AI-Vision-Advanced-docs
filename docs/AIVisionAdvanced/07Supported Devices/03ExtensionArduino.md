# Extension – Arduino
## Introduction
The Arduino library is written in C++ and communicates with the K210 AI Vision Sensor via the I²C interface.

Based on this library, users can develop programs that achieve higher efficiency and richer functionalities. This tutorial mainly introduces usage through the `Wire` I²C library, but it is not limited to `Wire`. You may also refer to the `override` example to implement usage in other environments.

## Quick Start
### Hardware Requirements  
| <!-- 这是一张图片，ocr 内容为： -->
![](img/Ar01.png) | <!-- 这是一张图片，ocr 内容为： -->
![](img/Ar02.png) |
| :---: | :---: |
| K210 AI Vision Sensor | Grove to 4-pin Dupont cable |
| <!-- 这是一张图片，ocr 内容为： -->
![](img/Ar03.png) | <!-- 这是一张图片，ocr 内容为： -->
![](img/Ar04.png) |
| Arduino Uno | Expansion Shield |


Software Requirements

| <!-- 这是一张图片，ocr 内容为： -->
![](img/Ar05.png) | <!-- 这是一张图片，ocr 内容为： -->
![](img/Ar06.png) |
| :---: | :---: |
| Arduino IDE | Vision Module API Library |


Refer to the Grove port pin definitions for correct wiring.

### Library Acquisition
You can download the required API library for the vision module from:

#### GitHub：
1. Visit [GitHub](https://github.com/cyc36880/Arduino_k210)
2. Navigate to the Releases section on the lower right.

