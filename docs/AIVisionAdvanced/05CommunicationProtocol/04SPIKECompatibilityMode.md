# SPIKE Compatibility Mode
When the communication protocol is switched to SPIKE mode, the module simulates the output of a SPIKE color sensor. The K210 will generate corresponding color values, reflectance, and RGB data based on the current AI recognition mode.

_***Note: **_When in SPIKE mode, the module must be connected to a SPIKE device. If not connected, the module will not function properly. To reset to factory settings: First, disconnect the power supply. Hold down the button without releasing it while plugging in a Type-C charger. Once the boot screen appears, release the button to restore default configurations.



When the port protocol is switched to SPIKE mode, the K210 simulates the output of a SPIKE color sensor. In different vision modes, the meaning of the color value, reflectance, and RGB values is as follows:

| **Mode** | **Color Value** | **Reflectance** | **R Value** | **G Value  ** | **B Value  ** |
| :---: | :---: | :---: | --- | --- | --- |
| Color Recognition | 9 | (R+G+B)/255×100 | Red component | Green component | Blue component |
| Color Block Tracking | 9 if found, -1 otherwise | Block W / 3 | 0 | Block X coordinate | Block Y coordinate |
| Apriltag Recognition | 9 if found, -1 otherwise | Tag W / 3  | Tag ID | Tag X coordinate | Tag Y coordinate |
| Line Recognition (lowest detected line only) | 9 if found, -1 otherwise | 0 | 0 | Line X coordinate | Line Y coordinate |
| 20-Class Object Recognition | 9 if found, -1 otherwise | Object W / 3  | Object ID | Object X coordinate | Object Y coordinate |
| QR Code Recognition | 9 if found, -1 otherwise | QR code W / 3 | 0 | QR code X coord. | QR code Y coord. |
| Face Recognition | 9 if found, -1 otherwise | Face W / 3 | 0 | Face X coord. | Face Y coord. |
| Face Attributes | 9 if a learned face detected, -1 otherwise | — | 1 = Mouth open / 0 = Closed | 1 = Smile / 0 = Neutral | 1 = Glasses / 0 = None |
| Deep Learning | Returns detected ID if found, otherwise -1 | — | — | — | — |
| Card Road Sign Recognition | Returns detected ID if found, otherwise -1 | Card W / 3 | Card ID | Card X coord. | Card Y coord. |
| AI Chat | **AI Status:**<br/>+ **0**: AI not started<br/>+ **1**: Connecting<br/>+ **2**: Standby<br/>+ **3**: Listening<br/>+ **4**: Speaking | **Commands:**<br/>+ **1**: Move Forward<br/>+ **2**: Move Backward<br/>+ **3**: Turn Left<br/>+ **4**: Turn Right<br/>+ **5**: Stop | **Speed:**   Range: **0-100** | **Custom Command:**   Range: **1-255** |  |
| WiFi Stream | **Connect to Wi-Fi:**<br/>+ **9**: Successfully connected to Wi-Fi<br/>+ **-1**: Failed to connect to Wi-Fi |  Image Transmission Keyboard Buttons <br/>0000 wasd |  Image Transmission Web Buttons<br/>0012 3456 |  Image Transmission Joystick：<br/>**X axis**:  0~200 | Image Transmission Joystick：<br/>**Y axis**:  <br/>0~200 |
| Settings | -1 | 0 | 0 | 0 | 0 |


Note:  

+ `<font style="background-color:rgba(255, 255, 255, 0.05);"> Color Value</font>`  Corresponds to the "Color Number" in the SPIKE protocol.  
+ `<font style="background-color:rgba(255, 255, 255, 0.05);">(R+G+B)/255×100</font>`  This is the calculation method for simulating reflectance, with results in the range of **0~100**.  
+ For unused fields (such as deep learning, Wi-Fi, etc.), the RGB values may be **0** or random.
+ **Line Recognition**: SPIKE can only capture the coordinates of the lowest recognized line.
+ **Image Transmission Web Joystick**: Two bytes represent the X and Y joystick values, with the midpoint being **100**.
+ **Image Transmission Web Buttons**: **0012 3456**; when the corresponding button is pressed, the respective bit is set to **1**.
+ **Image Transmission Keyboard Buttons**: **0000 wasd**; when the corresponding keyboard key is pressed, the respective bit is set to **1**.

  
 

