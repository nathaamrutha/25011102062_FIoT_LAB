# STM32 UART Communication with ESP8266

## 1. Aim
To establish UART communication between the STM32 microcontroller and an ESP8266 Wi-Fi module using USART1 and USART2, and display the received AT command response on a serial terminal.

## 2. Components Required
- STM32 microcontroller (STM32F103 series)
- ESP8266 Wi-Fi module
- USB-to-Serial converter / ST-Link
- Jumper wires
- Computer with STM32CubeIDE

## 3. Software Requirements
- STM32CubeIDE
- STM32CubeMX
- Embedded C
- HAL Library

## 4. Communication Configuration

| Parameter | USART1 | USART2 |
|---|---|---|
| Baud Rate | 115200 | 115200 |
| Word Length | 8 Bits | 8 Bits |
| Stop Bits | 1 | 1 |
| Parity | None | None |
| Mode | TX and RX | TX and RX |

## 5. Pin Connections

### STM32 to ESP8266

| STM32 Pin | ESP8266 Pin |
|---|---|
| USART1 TX (PA9) | RX |
| USART1 RX (PA10) | TX |
| GND | GND |

### STM32 to Serial Terminal

| STM32 Pin | USB-to-Serial Converter |
|---|---|
| USART2 TX (PA2) | RX |
| USART2 RX (PA3) | TX |
| GND | GND |

**Note:** Ensure that the ESP8266 receives a suitable 3.3V supply and that UART logic levels are compatible.

## 6. Working Principle

1. The STM32 microcontroller initializes the system clock and GPIO peripherals.
2. USART1 and USART2 are initialized with a baud rate of 115200.
3. The STM32 transmits the AT command `AT\r\n` to the ESP8266 through USART1.
4. The ESP8266 processes the AT command and sends its response through USART1.
5. The STM32 receives the response one byte at a time.
6. Each received byte is transmitted to the computer through USART2.
7. The response can be observed using a serial terminal.

## 7. Program Logic

- Initialize HAL and configure the system clock.
- Initialize GPIO, USART1 and USART2.
- Send the AT command to the ESP8266.
- Continuously receive data through USART1.
- Forward each received byte through USART2.

## 8. Expected Output

When the ESP8266 is connected and responding correctly, the serial terminal should display:

```text
AT
OK
```

The exact response may vary depending on the ESP8266 firmware.

## 9. Result

UART communication between the STM32 microcontroller and ESP8266 was implemented using USART1. The received response was forwarded to the computer through USART2 and displayed on the serial terminal.
