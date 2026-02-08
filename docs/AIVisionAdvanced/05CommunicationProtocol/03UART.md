# UART
## Serial Parameters
+ Baud rate: 115200
+ Data bits: 8
+ Parity: None
+ Stop bits: 1
+ Flow control: None

Ensure that the main controller or host computer uses the same configuration to enable proper communication.

## Data Packet
|  |  Header |  Packet Length | Data  | ... | Checksum |
| :---: | :---: | :---: | :---: | :---: | :---: |
| Byte Length | 3 | 2 | 2+ |  | 1 |
| Content | ICA |  | id+data_size+data |  | / |
| Description | “ICA”<br/>Fixed 3-byte header | High byte first, low byte next. Indicates the length of all data bytes following this field. | ID refers to command ID; data_size = length of data; data = payload |  | Calculated checksum |


> Note: A single data packet can contain multiple data objects, but the IDs must not be duplicated.
>

## Communication Process
Communication consists of read and write operations.

After each command is sent, the device returns an ACK response, reflecting the result of the last command.

### Command IDs
| Command | ID | Description |
| :---: | :---: | --- |
| Notify | 0 | Sent by device; the host only needs to check this command field |
| Write | 1 | 1 byte: target register address |
| Read | 2 | 2 bytes: address + data length |
| *Data | 10 | Used together with Write command; cannot be used alone |


### Response Codes
|  Description | Code |
| :---: | :---: |
|  Success | 0 |
|  Packet transmission timeout | 1 |
|  Transmission information is too long, exceeding buffer capacity | 2 |
|  Command error / No related command | 4 |
|  Missing data in the received packet | 7 |
|  Missing data in the received packet | 8 |
| Register error (No related register) | 9 |
|  System error | 10 |
|  Data type error | 11 |


Explanation:

+ **Packet transmission timeout**: This error occurs when the entire data packet is not received continuously. If the sender breaks the packet into multiple segments and the gap between segments is too long, this error will occur.
+ **Receiving complete, but checksum error**: This error happens when the entire data packet is received, but the checksum does not match. This can be caused by a bug in the sender's code or transmission errors due to environmental interference.
+ **System error**: This occurs when the system has not fully powered on, or there is an internal error during communication.

**Note**: If the first 5 bits (packet header + packet length) are not completely transmitted, no error will be triggered. After a timeout, the device will simply ignore the packet.



### Communication Example:  
**Host reads the device register value  **

 Host Sends:  `49 43 41` `00 05` `02 02 00 01` ` D7`

+ `49 43 41`:  Fixed packet header 
+ `00 05` ：Packet length  
+ `02 02 00 01` ：02， Read command ID； 02， Data length；00 01， Read address (ADDR=00), size=1
+ `D7` ： Checksum  



 Device Replies:  `49 43 41` `00 07` `00 01 00` `0A 01 02 ` `E2`

+  `49 43 41`: Fixed packet header 
+ `00 07` ：Packet length
+ `00 01 00` ： ID=0 (response command)  ; 01: Data length; Data: 00 (response status: ok) 
+ `0A 01 02` ：ID=10 (data command); Data length: 1; Data: 02
+ `E2` ： Checksum

