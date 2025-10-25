# Introduction to Sensor Service Kit Development  

## Usage Scenarios  

Sensor Service Kit enables applications to obtain raw data from sensors and provides vibration control capabilities.  

- The **Sensor** module is a device abstraction concept that allows applications to access underlying hardware sensors. Developers can subscribe to sensor data through the provided interfaces and customize corresponding algorithms based on the sensor data to develop various applications, such as compasses, fitness tracking, gaming, and more.  

## Constraints and Limitations  

### Sensor  

- To utilize sensor functionalities, the device must be equipped with the corresponding sensor hardware.  
- For certain sensors, developers need to request appropriate permissions to access the respective sensor data.  
- Sensor data subscription and unsubscription interfaces must be called in pairs. When sensor data is no longer required, developers must invoke the unsubscription interface to stop data reporting.