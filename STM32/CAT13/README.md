# EXPERIMENT DETAILS

**EXP:** CONTINUOUS ASSESSMENT 12

**NAME OF EXP:** BME280 Sensor Interfacing with STM32 using I2C Communication

**HARDWARE SETUP / PLATFORM:** STM32CubeMX + Keil MDK + STM32F401RE Development Board + BME280 Environmental Sensor

---

## TASK  – BME280 Sensor Interfacing using I2C and Bosch Sensor API

### 1. Circuit Diagram

The experiment demonstrates interfacing the BME280 environmental sensor with the STM32F401RE microcontroller using the I2C communication protocol.

The BME280 sensor measures temperature, atmospheric pressure, and relative humidity. The STM32 communicates with the sensor through the I2C1 peripheral to retrieve the environmental data.

**Hardware Components:**

- **Development Board:** STM32F401RE
- **Microcontroller IC:** STM32F401RE
- **Sensor:** BME280 Environmental Sensor
- **Communication Protocol:** I2C
- **I2C Peripheral:** I2C1
- **Additional Peripheral:** USART6

**Connections:**

- STM32 I2C1 SCL → BME280 SCL
- STM32 I2C1 SDA → BME280 SDA
- STM32 3.3V → BME280 VCC
- STM32 GND → BME280 GND

**I2C Configuration:**

- Clock Speed: 100 kHz
- Duty Cycle: I2C Duty Cycle 2
- Addressing Mode: 7-bit
- Primary I2C Address: BME280 Primary Address

**UART Configuration:**

- Baud Rate: 115200
- Word Length: 8 Bits
- Stop Bits: 1
- Parity: None
- Mode: Transmitter and Receiver

### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates reading temperature, pressure, and humidity values from the BME280 sensor using the STM32 HAL library and Bosch BME280 sensor driver.

The STM32 communicates with the BME280 through the I2C1 peripheral. The sensor driver is configured with custom I2C read, write, and delay callback functions.

Initially, the BME280 device structure is configured with its I2C address, communication interface, and callback functions. The sensor is then initialized using `bme280_init()`.

The sensor settings are configured with 1X oversampling for temperature, pressure, and humidity, with the internal filter disabled.

The sensor is placed in Normal Mode, allowing continuous measurement of environmental parameters.

Inside the infinite loop, the program retrieves all sensor data using `bme280_get_sensor_data()`.

The retrieved values are stored in variables:
- **Temperature:** Stored in the `temperature` variable.
- **Pressure:** Stored in the `pressure` variable after converting from Pa to hPa by dividing by 100.
- **Humidity:** Stored in the `humidity` variable.

A delay of 1000 milliseconds is introduced before the next sensor reading.

**Pseudocode:**

1. Initialize the HAL library.
2. Configure the system clock.
3. Initialize GPIO peripherals.
4. Initialize I2C1 with a clock speed of 100 kHz.
5. Initialize USART6 with a baud rate of 115200.
6. Configure the BME280 device address.
7. Set the communication interface to I2C.
8. Assign the custom I2C read, write, and delay callback functions.
9. Initialize the BME280 sensor using `bme280_init()`.
10. Configure temperature, pressure, and humidity oversampling to 1X.
11. Disable the internal filter.
12. Set the sensor to Normal Mode.
13. Continuously read all sensor data using `bme280_get_sensor_data()`.
14. Check whether the sensor data retrieval is successful.
15. Store the temperature value.
16. Convert pressure from Pa to hPa and store it.
17. Store the humidity value.
18. Introduce a delay of 1000 milliseconds.
19. Repeat the process continuously.

**Code Base:**

The sensor communication and data acquisition operations are performed using the following STM32 HAL functions and BME280 driver functions:

- `HAL_Init()` – Initializes the HAL library.
- `HAL_I2C_Init()` – Initializes the I2C1 peripheral.
- `HAL_I2C_Mem_Read()` – Reads data from the BME280 sensor registers.
- `HAL_I2C_Mem_Write()` – Writes configuration data to the BME280 sensor registers.
- `HAL_Delay()` – Introduces delays in milliseconds.
- `bme280_init()` – Initializes the BME280 sensor.
- `bme280_set_sensor_settings()` – Configures sensor oversampling and filter settings.
- `bme280_set_sensor_mode()` – Sets the sensor operating mode.
- `bme280_get_sensor_data()` – Retrieves temperature, pressure, and humidity measurements.

**Custom Callback Functions:**

- `user_i2c_read()` – Reads sensor register data through I2C using `HAL_I2C_Mem_Read()`.
- `user_i2c_write()` – Writes configuration data to sensor registers using `HAL_I2C_Mem_Write()`.
- `user_delay_us()` – Provides the delay required by the BME280 driver using `HAL_Delay()`.

**Important Variables:**

- `dev` – Stores BME280 device configuration and callback functions.
- `comp_data` – Stores the compensated sensor readings.
- `rslt` – Stores the status returned by BME280 driver functions.
- `temperature` – Stores the measured temperature.
- `pressure` – Stores the measured atmospheric pressure in hPa.
- `humidity` – Stores the measured relative humidity.

### 3. Inference

The STM32F401RE communicates successfully with the BME280 environmental sensor using the I2C1 communication protocol.

The sensor provides temperature, atmospheric pressure, and humidity measurements. The retrieved values are stored in their respective variables, and the program continuously updates the readings at intervals of 1 second.

This experiment demonstrates I2C communication, sensor interfacing, register read/write operations, sensor configuration, and environmental data acquisition using STM32 and the BME280 sensor.
