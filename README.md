# GSM Based Digital Notice Display with Emergency Alert using LPC2129

## 1. Project Overview

The GSM Based Digital Notice Display with Emergency Alert is an embedded systems project developed using the ARM7 LPC2129 microcontroller and SIM800C GSM module.

The system receives SMS messages from a mobile phone through the SIM800C GSM module. The received message is transferred to the LPC2129 microcontroller using UART communication and displayed on a 16×2 LCD.

The system checks the received SMS content to identify emergency messages. If the word **"EMERGENCY"** is present anywhere in the received message, the microcontroller activates a red LED and buzzer to indicate an emergency condition.

For normal messages that do not contain the emergency keyword, the message is displayed on the LCD and the green LED is activated.

A push button is used to turn OFF the buzzer during an emergency condition through GPIO input checking. The received SMS information is also transmitted to a PC through UART communication.

This project provides a wireless notification system with an additional emergency alert mechanism.

## 2. Objectives

- To develop a wireless digital notice display system using GSM technology.
- To receive SMS messages through the SIM800C GSM module.
- To display received messages on a 16×2 LCD.
- To identify emergency messages by checking the word "EMERGENCY" anywhere in the SMS.
- To activate a red LED and buzzer when an emergency message is detected.
- To indicate normal messages using a green LED.
- To control the emergency buzzer using a push button.
- To establish UART communication between the LPC2129, GSM module, and PC.

## 3. Features

- Wireless SMS reception using the SIM800C GSM module.
- Automatic message reception and processing.
- LCD-based digital notice display.
- Emergency keyword detection using the word "EMERGENCY".
- Emergency alert using a red LED and buzzer.
- Green LED indication for normal messages.
- Push-button-based buzzer control using GPIO input.
- UART communication between the GSM module and microcontroller.
- Received message monitoring through PC serial communication.
- Modular Embedded C programming.

## 4. Hardware Requirements

| Component | Purpose |
|---|---|
| LPC2129 ARM7 Microcontroller | Main processing unit |
| SIM800C GSM Module | Wireless SMS communication |
| SIM Card | GSM network connectivity |
| 16×2 LCD Display | Displays received messages |
| Red LED | Emergency indication |
| Green LED | Normal message indication |
| Buzzer | Audio emergency alert |
| Push Button | Buzzer control |
| MAX3232 | RS-232 voltage-level conversion, where required |
| Power Supply | Provides required operating voltage |
| Connecting Wires | Circuit connections |

## 5. Software Requirements

| Software | Purpose |
|---|---|
| Keil µVision | Embedded C coding and compilation |
| Proteus 8.13 | Circuit design and simulation |
| Flash Magic | Programming the LPC2129 |
| Embedded C | Microcontroller programming |
| UART | Serial communication |
| GSM AT Commands | GSM module configuration and control |

## 6. Pin Connections

The LPC2129 communicates with the external devices using its GPIO pins and UART peripheral.

| Module | LPC2129 Connection | Function |
|---|---|---|
| SIM800C(GSM) TX | UART0 RXD | Receives serial data |
| SIM800C(GSM) RX | UART0 TXD | Transmits serial data |
| LCD RS | GPIO | Register selection |
| LCD Enable | GPIO | LCD enable control |
| LCD Data Lines | GPIO | Transfers display data |
| Red LED | GPIO output | Emergency indication |
| Green LED | GPIO output | Normal indication |
| Buzzer | GPIO output | Audio alert |
| Push Button | GPIO input | Buzzer control |

The exact GPIO pin assignments depend on the circuit configuration and source code.

## 7. Working Principle

The system works by receiving SMS messages through the SIM800C GSM module and processing them using the LPC2129 ARM7 microcontroller.

### Step 1: System Initialization

- Initially, the LPC2129 microcontroller is powered ON.
- The GPIO pins are configured for the LCD, LEDs, buzzer, and push button.
- UART communication is initialized for communication with the GSM module.
- The LCD is initialized to display the received messages.
- The SIM800C GSM module is initialized using AT commands.
- After completing initialization, the system waits for incoming SMS messages.

### Step 2: SMS Reception

- The user sends an SMS from a mobile phone to the SIM card inserted in the SIM800C module.
- The SIM800C module receives the SMS through the GSM network.
- The received SMS information is transferred to the LPC2129 through UART communication.
- The microcontroller receives the serial data and extracts the message content.
- The received message is passed to the message-processing section.

### Step 3: Message Processing and Keyword Detection

- The LPC2129 checks the content of the received SMS.
- The microcontroller searches for the word **"EMERGENCY"** anywhere in the received message.
- The keyword is not required to appear only at the beginning of the message.
- If the word is found anywhere in the SMS, the message is classified as an emergency message.
- If the word is not found, the message is treated as a normal message.

**Example Messages:**

| Received SMS | Message Type |
|---|---|
| Meeting at 10 AM | Normal |
| EMERGENCY: Fire detected | Emergency |
| Please respond, this is an EMERGENCY | Emergency |
| EMERGENCY situation near the entrance | Emergency |
| Welcome to the event | Normal |

### Step 4: Normal Message Display

When the received message does not contain the word "EMERGENCY":

- The microcontroller identifies it as a normal notification.
- The received message is displayed on the 16×2 LCD.
- The green LED is switched ON.
- The red LED remains OFF.
- The buzzer remains OFF.
- The received message information is transmitted to the PC through UART.

### Step 5: Emergency Message Detection and Alert

When the received SMS contains the word "EMERGENCY" anywhere in its content:

- The microcontroller identifies the message as an emergency notification.
- The received message is displayed on the LCD.
- The red LED is switched ON.
- The buzzer is activated to generate an audible alert.
- The green LED remains OFF.
- The emergency message information is transmitted to the PC through UART.
- The emergency buzzer remains active until it is switched OFF using the push button.

### Step 6: Push Button-Based Buzzer Control

- A push button is connected to a GPIO input pin of the LPC2129.
- The microcontroller continuously checks the push-button input in the program.
- When the button is pressed, the microcontroller detects the input condition.
- The buzzer is switched OFF through the normal program execution.
- This allows the user to control the emergency buzzer without restarting the complete system.

## 8. GSM Module – SIM800C

The SIM800C is a GSM/GPRS communication module used for wireless communication through a cellular network.

It supports SMS communication, voice communication, and GPRS data transfer.

In this project, the SIM800C is used to receive SMS messages from a mobile phone and transfer the received information to the LPC2129 microcontroller through UART communication.

The module is controlled using AT commands sent by the microcontroller.

### Important AT Commands

| AT Command | Description |
|---|---|
| `AT` | Checks communication with the GSM module |
| `ATI` | Displays module identification |
| `AT+CSQ` | Checks GSM signal quality |
| `AT+CMGF=1` | Configures SMS text mode |
| `AT+CNMI` | Configures new SMS notification |
| `AT+CMGR` | Reads a received SMS |
| `AT+CMGL` | Lists received SMS messages |

These commands are used according to the SMS reception method implemented in the firmware.

## 9. Communication Protocol

### UART (Universal Asynchronous Receiver Transmitter)

UART is a serial communication protocol used to transfer data between electronic devices.

In this project, UART is used for communication between the LPC2129 microcontroller and SIM800C GSM module.

**UART Communication Between LPC2129 and SIM800C:**

- The LPC2129 sends AT commands to the GSM module.
- The GSM module responds to the commands.
- Incoming SMS information is transferred to the microcontroller.
- The microcontroller processes the received serial data.

**UART Communication Between LPC2129 and PC:**

- The microcontroller transmits received message information to the PC.
- The transmitted data can be monitored using a serial terminal.
- This communication is useful for monitoring and debugging.

### GPIO (General Purpose Input/Output)

GPIO pins are used to control the red LED, green LED, and buzzer.

The push button is also connected to a GPIO input pin. The microcontroller checks its input state to control the buzzer.

The output states are changed depending on whether the received message is normal or an emergency.

## 10. Expected Output

The system produces different outputs depending on the content of the received SMS.

### Case 1: Normal Message

**Input SMS:**

`Meeting will start at 10 AM`

**Expected Result:**

- LCD displays the received message.
- Green LED turns ON.
- Red LED remains OFF.
- Buzzer remains OFF.
- Message information is transmitted to the PC.

### Case 2: Emergency Message

**Input SMS:**

`EMERGENCY: Fire accident detected`

**Expected Result:**

- LCD displays the received message.
- Red LED turns ON.
- Buzzer turns ON.
- Green LED remains OFF.
- Emergency message information is transmitted to the PC.

### Case 3: Emergency Keyword in the Middle of the Message

**Input SMS:**

`Please take action immediately. This is an EMERGENCY situation.`

**Expected Result:**

- The microcontroller detects the word "EMERGENCY".
- Red LED turns ON.
- Buzzer turns ON.
- The message is displayed on the LCD.

### Case 4: Buzzer Deactivation

- When the push button is pressed, the GPIO input state is detected by the microcontroller.
- The buzzer turns OFF.
- The emergency message remains available for display.

## 11. Applications

- Wireless digital notice boards.
- Emergency notification systems.
- Industrial warning systems.
- Public information display systems.
- Remote announcement systems.
- Safety monitoring systems.
- Wireless communication-based alert systems.

## 12. Limitations and Future Enhancements

### Limitations

- The system depends on GSM network availability.
- SMS delivery may experience network delays.
- The LCD has limited message display capacity.
- The GSM module requires a suitable power supply.
- Emergency detection depends on the specified keyword.
- Messages containing the keyword in an unrelated context may also trigger an emergency alert.

### Future Enhancements

- Support for multiple authorized mobile numbers.
- Add scrolling functionality for longer messages.
- Implement sender authentication.
- Add automatic SMS acknowledgement.
- Store received messages for future reference.
- Integrate IoT technology for remote monitoring.
- Add additional emergency notification mechanisms.

## 13. Advantages

- Provides wireless notification through GSM technology.
- Eliminates the need for manual notice updates.
- Automatically detects emergency messages.
- Provides both visual and audio alerts.
- Allows simple buzzer control using a push button.
- Enables PC monitoring using UART communication.
- Uses an ARM7 microcontroller for message processing.
- Demonstrates practical embedded system interfacing concepts.

## 14. How to Run the Project

1. Download or clone the project repository.
2. Open the project using Keil µVision.
3. Add all required Embedded C source files and header files.
4. Select the LPC2129 microcontroller as the target device.
5. Build the project and verify that there are no compilation errors.
6. Generate the HEX file from the Keil project.
7. Open the Proteus circuit and verify all hardware connections.
8. Load the generated HEX file into the microcontroller in Proteus, if using simulation.
9. For hardware testing, program the LPC2129 using Flash Magic.
10. Ensure that the SIM800C module has a proper power supply, SIM card, and GSM network connectivity.
11. Power ON the system and wait for GSM initialization.
12. Send a normal SMS to the SIM800C module.
13. Observe the LCD message and green LED indication.
14. Send an SMS containing the word "EMERGENCY".
15. Observe the red LED and buzzer activation.
16. Press the push button to deactivate the buzzer.
17. Monitor the received message information through the PC serial terminal.

## 15. Conclusion

The GSM-Based Digital Notice Display with Emergency Alert using LPC2129 provides a wireless notification system using the SIM800C GSM module.

The system receives SMS messages, displays them on an LCD, and identifies emergency messages using the keyword "EMERGENCY". It activates a red LED and buzzer for emergency alerts, while a push button provides buzzer control.

This project demonstrates practical implementation of Embedded C programming, GSM interfacing, UART communication, GPIO control, and ARM7 microcontroller technology.
