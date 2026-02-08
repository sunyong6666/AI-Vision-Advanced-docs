# IIC
## Device Address
Supports three selectable addresses: `0x24、``0x25、``0x26`

The address can be selected in the Settings interface.

After configuration, the device will automatically restart to apply the new address, preventing conflicts with other I²C devices.

## Registers
### Register Description
+ All registers are read/write (in principle). However, writing to registers that should not be modified may trigger unintended actions.
+ The actual register address =`Function Base Address`+`Register Offset`
+ Unless otherwise specified, registers are initialized to `0` after power-on.
+ Reading/writing non-existent registers or out-of-range values will return 0.
+ Multi-byte numbers are stored in **big-endian format** (high byte first, low byte last).
+ Before writing to registers, ensure that the `AI Vision Sensor` is in the corresponding function interface.

| Function | Base Address |
| :---: | :---: |
| System Settings | 0 |
| Color Detection | 15 |
| Color Block Tracking | 30 |
| Apriltag Recognition | 45 |
| Line Recognition | 60 |
| 20-Class Object Recognition | 75 |
| QR Code Recognition | 90 |
| Face Attributes Recognition | 105 |
| Face ID Recognition | 120 |
| Deep Learning | 135 |
| Card Recognition | 150 |
| ESP | 165 |
| Settings | 180 |


### Register Table  
#### sys (System Registers)
| Offset | Description | Length (bytes) |
| :---: | --- | :---: |
| 0x00 | Operating mode (0–9) | 1 |
| | 0: Color Recognition | |
| | 1: Color Block Tracking | |
| | 2: Apriltag Recognition | |
| | 3: Line Recognition | |
| | 4: 20-class Object Recognition | |
| | 5: QR Code Recognition | |
| | 6: Face Attributes Recognition | |
| | 7: Face ID Recognition	 | |
| | 8: Deep Learning	 | |
| | 9: Card Road Sign Recognition | |
| | 10: WIFI Stream | |
| 0x01 | Boot verification (value: 9876543210123456789; returns 0 if not fully booted) | 19 |
| 0x02 | SD card detection (0: none, 1: detected) | 1 |
| 0x03 | ESP32-S3 communication status (0: error, 1: normal) | 1 |


### get_color (Color Detection)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | Average RGB color at screen center<br/>(r,g,b; each 0–255) | 3 |
| | | |


### find_color (Color Block Tracking)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | The ID of the color to be tracked. Range: 1 ~ 6 | 1 |
| | | |
| 0x01 | Indicates whether the target color block is detected. 0 = Not found, 1 = Found | 1 |
| | | |
| 0x02 | Provides detailed information of the detected color block. x, y, w, h (2 bytes each) | 8 |
| | | |


> id 1~6
>
> Red, green, blue, yellow, black and white
>



### find_tag (Apriltag Recognition)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | Number of tags detected | 1 |
| 0x01 | Number of tags detected | 12 |
| 0x02 | Number of tags detected | 12 |
| 0x03 | Number of tags detected | 12 |
| 0x04 | Tag information<br/>id (2), rotation (2), x, y, w, h (each 2 bytes) | 12 |


> rotation: 0 ~ 359
>

### find_line (Line Recognition)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | Line detection flag<br/>0 = Not detected, 1 = Detected | 1 |
| | | |
| 0x01 | Line information<br/>x, y, w, h (each 2 bytes) | 8 |
| 0x02 | Line information<br/>x, y, w, h (each 2 bytes) | 8 |
| 0x03 | Line information<br/>x, y, w, h (each 2 bytes) | 8 |


### find_20_class (20-Class Object Recognition)
```plain
0: Airplane
1: Bicycle
2: Bird
3: Boat
4: Bottle
5: Bus
6: Car
7: Cat
8: Chair
9: Cow
10: Dining Table
11: Dog
12: House
13: Motorcycle
14: Person
15: Potted Plant
16: Sheep
17: Sofa
18: Train
19: TV Monitor
```

| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | Number of objects detected | 1 |
| 0x01 | Number of objects detected | 9 |
| 0x02 | Number of objects detected | 9 |
| 0x03 | Number of objects detected | 9 |
| 0x04 | Object information<br/>id (1), x, y, w, h (each 2 bytes) | 9 |


> ID starts from 0, corresponding to the following objects in order:
>

### find_qrcode (QR Code Recognition)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | QR code detection flag<br/>0 = Not detected, 1 = Detected | 1 |
| | | |
| 0x01 | QR code data length | 1 |
| 0x02 | QR code bounding box<br/>x, y, w, h (each 2 bytes) | 8 |
| 0x03 | QR code information | 100 |


### find_face (Face Attributes)
| Offset | Description | Length (bytes) |
| :---: | --- | :---: |
| 0x00 | Number of faces detected | 1 |
| 0x01 | Face 1  x, y, w, h (each 2 bytes) | 8 |
| 0x02 | Face 2  x, y, w, h (each 2 bytes) | 8 |
| 0x03 | Face 3  x, y, w, h (each 2 bytes) | 8 |
| 0x04 | Face 4  x, y, w, h (each 2 bytes) | 8 |
| 0x05 | Face 1 attributes<br/>is_male(deprecated but reserved), is_mouth_open, is_smail, is_glasses | 4 |
| 0x06 | Face 2 attributes<br/>is_male(deprecated but reserved), is_mouth_open, is_smail, is_glasses | 4 |
| 0x07 | Face 3 attributes<br/>is_male(deprecated but reserved), is_mouth_open, is_smail, is_glasses | 4 |
| 0x08 | Face 4 attributes<br/>is_male(deprecated but reserved), is_mouth_open, is_smail, is_glasses | 4 |


### find_face_recognition (Face ID Recognition)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | Number of faces detected | 1 |
| 0x01 | Number of faces recognized | 1 |
| 0x02 | Face 1 info    id (1), x, y, w, h (each 2 bytes)   | 9 |
| 0x03 | Face 2 info    id (1), x, y, w, h (each 2 bytes)   | 9 |
| 0x04 | Face 3 info    id (1), x, y, w, h (each 2 bytes)   | 9 |
| 0x05 | Face 4 info    id (1), x, y, w, h (each 2 bytes)   | 9 |


> Detection count: The total number of faces framed on the screen.
>
> Recognition count: The number of faces successfully matched from the learned dataset.
>

### self_lenrning  (Deep Learning)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | (Deep Learning)<br/>0 = No, 1 = Yes | 1 |
| 0x01 | Detection flag<br/>0 = Not detected, 1 = Detected | 1 |
| 0x02 | ID of recognized object (0–1) | 1 |
| | | |


### find_card (Card Road Sign Recognition)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | Number of cards detected（0-4） | 1 |
| 0x01 | Card 1 info<br/>id (1), x, y, w, h (each 2 bytes) | 9 |
| 0x02 | Card 2 info<br/>id (1), x, y, w, h (each 2 bytes) | 9 |
| 0x03 | Card 3 info<br/>id (1), x, y, w, h (each 2 bytes) | 9 |
| 0x04 | Card 4 info<br/>id (1), x, y, w, h (each 2 bytes) | 9 |


Note：ID Mapping (0–6):

0: Green Light; 1: Left Turn; 2: Stop; 3: Red Light; 4: Right Turn; 5: Horn; 6: Target

### ESP (AI Chat & WIFI Stream)
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | wifi ssid<br/>The first byte indicates the length of the SSID, followed by the SSID string | 100 |
| | | |
| 0x01 | wifi password<br/>The first byte indicates the length of the password, followed by the password string | 100 |
| | | |
| 0x02 | wifi ip<br/>The first byte indicates the length of the IP, followed by the IP address | 20 |
| | | |
| 0x03 | <font style="color:#DF2A3F;"> Reserved</font> | 1 |
| 0x04 |  AI XiaoZhi Status   | 1 |
| 0x05 |  Motion Command | 1 |
| 0x06 |  Custom Command | 1 |
| 0x07 |  Image Transmission Web Joystick | 2 |
| 0x08 |  Image Transmission Web Button | 1 |
| 0x09 | Image Transmission Keyboard Button | 1 |


> **P**: An IP of **0.0.0.0** or an IP length of **0** indicates that the device is not connected to Wi-Fi.  
>
> **AI XiaoZhi Status**:
>
> + 0: AI not started
> + 1: Connecting
> + 2: Standby
> + 3: Listening
> + 4: Speaking
> + 5: Network configuration in progress
> + **Image Transmission Web Joystick**:  
Two bytes represent the X and Y joystick values, with a range from **-100 to 100**.
> + **Image Transmission Web Button**:  
"0012 3456"; returns one byte. When a corresponding button is pressed, the respective bit is set to **1**.
> + **Image Transmission Keyboard Button**:  
"0000 wasd"; returns one byte. When a corresponding keyboard key is pressed, the respective bit is set to **1**.
>

### setting
| Offset | Description | Length (bytes) |
| :---: | :---: | :---: |
| 0x00 | Fill light brightness<br/>Range: 0–10 | 1 |
| 0x01 | Fill light switch<br/>0 = Off, 1 = On | 1 |
| 0x02 | <font style="color:red;">Factory test (do not use)</font>   When set to 1, the module will automatically cycle through modes on the next startup; long press to exit test mode | 1 |
| 0x03 | <font style="color:green;">Language (read-only)</font>   0 = Chinese, 1 = English | 1 |
| 0x04 | <font style="color:green;">Control chip (read-only)</font>   0 = K210, 1 = ESP32 | 1 |


