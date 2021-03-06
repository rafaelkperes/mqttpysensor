# Installation and Setup
Required components:
- MQTT broker Mosquitto
- MongoDB
- Tomcat8
- Python3
- Python modules: paho-mqtt, pymongo
- Maven

## Linux 
- Run script install.sh
- Run value-logger.py

On the browser: http://localhost:8080/MBP

## Windows
- Install and start Mosquitto, MongoDB and Tomcat8
- Install Python3 and download paho-mqtt, pymongo (pip install ...)
- Build with maven the project .war file (mvn clean install)
- Deploy application on tomcat by moving .war to Tomcat8 webapps folder

On the browser: http://localhost:8080/restful-connde

# Registering Devices, Sensor and Actuator
On expert mode, register type and register device.

On normal mode or expert mode, register the component (sensor or device). 
The component id can be found in its url by selecting the component in the GUI. 

For example in the following URL, '596cafaa6c0ccd5d29da0e90' corresponds to the id:
http://localhost:8080/restful-connde/view/sensors/596cafaa6c0ccd5d29da0e90


# Sending Data to the Platform

To push values to the platform, use a MQTT client to push data to the topics 'sensor/$id' and 'actuator/$id', in which $id corresponds to the component id generated on the registration step.

The message format is a json string containing at least:
 - "component" : [ "SENSOR", "ACTUATOR" ] <- one of the values, accordingly
 - "id" : $id <- component id
 - "value" : $value

## Example:

$ mosquitto_pub.exe -t sensor/596cafaa6c0ccd5d29da0e90 -m '{"component": "SENSOR", "id": "596cafaa6c0ccd5d29da0e90", "value": 20}'
