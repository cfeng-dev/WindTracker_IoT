# WindTracker_IoT

WindTracker_IoT is an intelligent, real-time, and internet-enabled project designed for monitoring wind conditions. Using an [Ecowitt WS90](https://www.ecowitt.com/shop/goodsDetail/287) wind sensor, it collects data on wind speed and direction. This data is acquired via Modbus RTU 485 communication and then transmitted to a broker via MQTT. A notable feature of the WindTracker_IoT project is its ability to store data offline. When there is no internet connection, the system stores the collected data along with a timestamp on an SD card. Once the internet connection is restored, the system retrieves the stored data and republishes it via the broker. This design ensures no data is lost and provides reliable monitoring of wind conditions regardless of internet availability.

## Functionality

-   **Data Collection:** The program collects wind speed and direction data using an Ecowitt WS90 Wind Sensor and Modbus RTU 485 communication.
-   **Data Publishing:** Collected data is published via MQTT when internet access is available.
-   **Data Structuring:** Data is structured in JSON format before publishing, ensuring a standardized and efficient format for data transmission.
-   **Data Storage:** In case of internet unavailability, the system saves data onto an SD card with a timestamp.
-   **Resilient Publishing:** Upon re-establishing an internet connection, the stored data is published via MQTT broker.
-   **Task Management:** The system has been integrated with FreeRTOS to run multiple tasks concurrently, thereby improving overall efficiency.
-   **System Monitoring:** A Watchdog task continuously monitors the entire system. If the Watchdog isn't "fed" within a specific period, it initiates a system reset to prevent possible malfunctions.

## Libraries Used

-   **ArduinoModbus** and **ArduinoRS485** for Modbus communication.
-   **MKRNB** and **ArduinoMqttClient** for MQTT data publishing.
-   **SD** and **RTCZero** for data storage with timestamps.
-   **FreeRTOS_SAMD21** for concurrent task management.
-   **wdt_samd21** for implementing a Watchdog task for system monitoring.
-   **ArduinoJson** for structuring data in JSON format for efficient processing and transmission.

## Hardware Requirements

-   MKR NB 1500
-   Ecowitt WS90 Wind Sensor
-   MKR SD Proto Shield
-   MKR 485 Shield

## Circuit Configuration

-   Y connected with A (Green) of the Modbus RTU sensor
-   Z connected with B (White) of the Modbus RTU sensor
-   Jumper positions:
    -   A W B set to OFF
    -   FULL set to OFF
    -   Z W Y set to ON

## Software Requirements

-   Arduino IDE (version 2.1.1)
-   Arduino Libraries:
    -   ArduinoModbus (version 1.0.8)
    -   ArduinoRS485 (version 1.0.5)
    -   ArduinoMqttClient (version 0.1.7)
    -   MKRNB (version 1.5.1)
    -   SD (version 1.2.4)
    -   RTCZero (version 1.6.0)
    -   FreeRTOS_SAMD21 (version 2.3.0)
    -   wdt_samd21 (version 1.1.0)
    -   ArduinoJson (version 6.21.3)

## MQTT Broker Configuration

-   Broker: test.mosquitto.org
-   Port: 1883
-   Topics:
    -   `Sensor_KN/Winddata` for wind data
    -   `Sensor_KN/Error` for error messages

## Author

C.Feng, 2023
