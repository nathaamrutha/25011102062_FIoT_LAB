# EXPERIMENT DETAILS

**EXP:** CONTINUOUS ASSESSMENT 14

**NAME OF EXP:** MQTT Communication using STM32 and ESP8266 with Public MQTT Broker

**HARDWARE SETUP / PLATFORM:** STM32CubeMX + Keil MDK + STM32F401RE Development Board + Wemos ESP8266 Wi-Fi Module + EMQX MQTT Broker

---

## TASK 10 – BME280 Sensor Interfacing using I2C and (MQTT) Custom Built ESP8266 API

### 1. Circuit Diagram

The experiment demonstrates MQTT-based communication using the STM32F401RE microcontroller and Wemos ESP8266 Wi-Fi module.

The STM32 communicates with the ESP8266 through USART6. The ESP8266 connects to a Wi-Fi network and establishes a TCP connection with the public EMQX MQTT broker. The STM32 then publishes messages to a specified MQTT topic using the MQTT protocol.

**Hardware Components:**

- **Development Board:** STM32F401RE
- **Microcontroller IC:** STM32F401RE
- **Wi-Fi Module:** Wemos ESP8266
- **UART Peripheral:** USART6
- **Communication Protocol:** MQTT
- **MQTT Broker:** broker.emqx.io
- **MQTT Port:** 1883
- **MQTT Client ID:** STM32_Publisher
- **MQTT Topic:** stm32/amruthas/data

**Connections:**

- STM32 USART6 TX → Wemos ESP8266 RX
- STM32 USART6 RX → Wemos ESP8266 TX
- STM32 GND → Wemos GND
- Ensure that the ESP8266 is supplied with a suitable 3.3V power source.

**UART Configuration:**

- Baud Rate: 115200
- Word Length: 8 Bits
- Stop Bits: 1
- Parity: None
- Mode: Transmitter and Receiver

**MQTT Configuration:**

- Broker Address: broker.emqx.io
- Port: 1883
- Client ID: STM32_Publisher
- Keep Alive: 500
- Clean Session: Enabled
- Quality of Service (QoS): 0

### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates MQTT message publishing using the STM32F401RE microcontroller and Wemos ESP8266 Wi-Fi module with the public EMQX MQTT broker.

The STM32 communicates with the ESP8266 through USART6 using the ESP8266 library (ESPLib).

Initially, the ESP8266 is initialized in Station Mode and connected to the Wi-Fi network using the `ESP8266_Init()` and `ESP8266_wifiConnect()` functions.

After establishing Wi-Fi connectivity, the ESP8266 creates a TCP connection with the public MQTT broker `broker.emqx.io` on port 1883 using `ESP8266_portConnect()`.

The MQTT client is configured with the following parameters:

- Keep Alive: 500
- Clean Session: Enabled
- Client ID: STM32_Publisher

The MQTT connection with the broker is established using `MQTT_connectBroker()`.

Once connected, the STM32 continuously publishes the message **"Hi from IoT-B"** to the MQTT topic `stm32/amruthas/data` using `MQTT_publishTopic()` with QoS 0.

A delay of 1000 milliseconds is introduced between consecutive message publications.

**Pseudocode:**

1. Initialize the HAL library.
2. Configure the system clock.
3. Initialize GPIO peripherals.
4. Initialize USART6 with a baud rate of 115200.
5. Initialize the ESP8266 module in Station Mode.
6. Connect the ESP8266 to the Wi-Fi network using the SSID and password.
7. Establish a TCP connection with the EMQX MQTT broker at `broker.emqx.io` on port 1883.
8. Configure MQTT parameters:
   - Set Keep Alive to 500.
   - Enable Clean Session.
   - Set Client ID to STM32_Publisher.
9. Establish the MQTT connection with the broker.
10. Enter the infinite loop.
11. Publish the message "Hi from IoT-B" to the topic `stm32/amruthas/data`.
12. Use QoS level 0 for message delivery.
13. Introduce a delay of 1000 milliseconds.
14. Repeat the publishing process continuously.

**Code Base:**

The Wi-Fi and MQTT communication operations are performed using the following STM32 HAL and ESP8266 library functions:

- `HAL_Init()` – Initializes the HAL library.
- `HAL_UART_Init()` – Initializes the USART6 peripheral.
- `ESP8266_Init()` – Initializes the ESP8266 module in the specified Wi-Fi mode.
- `ESP8266_wifiConnect()` – Connects the ESP8266 to the specified Wi-Fi network.
- `ESP8266_portConnect()` – Establishes a TCP connection with the MQTT broker.
- `MQTT_connectBroker()` – Establishes the MQTT connection with the broker.
- `MQTT_publishTopic()` – Publishes messages to the specified MQTT topic.
- `HAL_Delay()` – Introduces a delay of 1000 milliseconds between publications.

**Important Variables and Structures:**

- `huart6` – UART handle used for communication with the ESP8266.
- `mqttSetting` – Stores the MQTT client configuration.
- `mqttSetting.keepAlive` – Specifies the MQTT keep-alive interval.
- `mqttSetting.connectFlag` – Configures the clean session option.
- `mqttSetting.clientID` – Specifies the unique MQTT client identifier.

### 3. Inference

The STM32F401RE successfully communicates with the Wemos ESP8266 through USART6 and establishes an MQTT connection with the public EMQX broker.

The STM32 continuously publishes the message "Hi from IoT-B" to the MQTT topic `stm32/amruthas/data` at intervals of one second using QoS 0.

The published messages can be monitored using an MQTT client such as MQTTX by connecting to the same broker and subscribing to the same topic.

This experiment demonstrates Wi-Fi connectivity, MQTT broker communication, TCP connection establishment, and real-time IoT message publishing using STM32 and ESP8266.
