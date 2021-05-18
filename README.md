# Artemis-Blue

# Outdoor GPS Dead-Reckoning with Lorawan

## Team Members

| Name | Role |
| ----------- | ----------- |
| Rhys Sneddon |  |
| Mairah Zulkepli |  |

## Project Overview
### Project Description
The purpose of this project is to build an outdoor GPS dead-reckoning with lorawan. It involves tracking a person using the Dragino Lorawan Module. A static beacon network will be created using the thing:52 for RSSI ranging and a dead-reckoning model with kalman filtering will be used. Lastly, a web dashboard viewer showing the current location will also be created. 

### Key Performance Indicator
The key performance indicators of the project would be:
1. Able to send gps location data from the LoRaWAN gps tracker to the Dragino gateway without much packet loss, latency and jitter (QoS is used)
2. Having a web dashboard viewer showing the general location of the person
3. At least be able to track a person in a 10 x 10 m outdoor area
4. Working static beacon network that is able to receive location data from the LoRaWAN gps tracker
5. Dead-reckoning model with kalman filtering works and is able to narrow down location of a person

### System Overview
** Block Diagram **
![alt text](image.jpg)

### Sensor Integration

### Wireless Network Integration
** Bluetooth network **
To facilitate RSSI ranging, the Thingy52 static nodes transmit bluetooth advertisements with the following payload format:

| Byte | 0 | 1 |
| ----------- | ----------- |
| Description | Preamble | Static Node ID |
| Value | 0b0011100 | e.g. 0x01 |

The Particle Argon scans for these advertisements as per the following message protocol diagram:
![alt text](image.jpg)

** LoRaWAN network **

GPS and RSSI and accelerometer data is sent to the LoRaWAN gateway via LoRaWAN as per the following payload formats and message protocol diagram:

** GPS and accelerometer data message payload (18 bytes) **

| Size (bytes) | 4 | 4 | 2 | 1 | 2 | 2 | 1 | 2 | 
| ----------- | ----------- |
| Description | Latitude | Longitude | Alarm and battery | Flags | Roll | Pitch | HDOP | Altitude |

** RSSI data message payload (4 bytes) **

| Size (bytes) | 1 | 1 | 1 | 1 |
| ----------- | ----------- |
| Description | RSSI of Static Node 1 | RSSI of Static Node 2 | RSSI of Static Node 3 | RSSI of Static Node 4 | 
![alt text](image.jpg)

### Algorithms
Dead-reckoning model with kalman filtering will be used to estimate the location of the mobile node. This is done by first having a known location of the node and then calculating an estimated location of the node by using the previous known location and the two rssi values received from the thingy:52. In order to increase the accuracy of the estimated location, Kalman filter is then used.

### Equipment
- LGT92 LoRaWAN GPS Tracker
- Dragino Gateway
- 2 Thingy:52
- 2 Particle Argons

### Progress
- Researched more about dead-reckoning model
- Found tutorials on using the LoRaWAN GPS Tracker