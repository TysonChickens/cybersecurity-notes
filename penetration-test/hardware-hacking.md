# Hardware Hacking

## Objectives

* [ ] Understand how data is sent via electrical wires in low-level hardware.
* [ ] Hardware communication protocols.
* [ ] Analyze hardware communication protocols.
* [ ] Reading USART data from a logic capture.

In the world of microchips, communication protocols are efficient as possible, and chips are made to be simple as possible. The worlds of 0s and 1s and how hardware takes electricity to generate signals is analyzed by a device called a Logic Analyzer. This device can be connected to the actual electrical wires that are used for communication between two devices that will capture and interpret the signals being sent.

## Electrical Heartbeat

Hardware components quickly power on and off to generate a digital signal - 1s and 0s bits. To perform communication, devices power on and off in a specific sequence to transmit a bunch of 0s and 1s.

* Sending 8 bits = 1 byte.

We can transmit data by using the [ASCII table](https://www.asciitable.com/). Consider that a single character is one byte of data (8 electrical wires). For this to be more efficient, requires fewer wires and then have both hardware chips agree to a specific digital protocol and configuration will be used to transmit data.

### USART

Universal Synchronous/Asynchronous Receiver-Transmitter (USART) communication, better known as serial communication, is a protocol that uses two wires. One wire is used to transmit (TX) data from Device A to Device B, and the other wire is used to receive (RX) data on Device A from Device B. The connection is established from transmit port from one device to the receive port from the other device and vice versa.

The interesting part of the protocol is there is no clock line to synchronize the communication of the devices. Without a clock, the devices have to agree to the configuration of comunication:

* **Communication** speed - Called the baud rate or bit rate and dictates how fast bytes of data can be sent. A specific rate tells each device how fast it should sample the data to get accurate communication.
* **Bits per transmission** - Normally set to 8 bits which makes a byte, but can be configured to something else such as 16 bits.
* **Stop and Start Bits** - Since there is no clock, one device has to send a signal to the other device before it can send or end a data transmission.
* **Parity Bits** - Since there can be errors in the communication, parity bits can be used to detect and correct errors in the transmission.

Once the two devices agree on the configuration of the serial lines, they can now communicate with each other.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/b1c981a472ba20b8cfa63b8b979ab156.png" alt=""><figcaption><p>Diagram ASCII character of "S" transmitted (USART).</p></figcaption></figure>

Some USART connections will use two additional lines called Clear to Send (CTS) and Request to Send (RTS) to communicate when the other device is ready to receive or ready to transmit. Furthermore, to agree on a voltage level is a binary 1 or 0, a 3rd wire called the Ground (GND) wire is required to allow the devices to have the same voltage reference.

### SPI

The Serial Peripheral Interface (SPI) communication protocol is mainly used for communication between microprocessors and small peripherals such as as sensor or an SD card. SPI uses a separate clock wire compared to USART communication with the clock built into the TX and RX lines. A separate clock (SCK) from the data (DATA) line allows for synchronous communication, which is faster and more reliable.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/d2a62b649df7a735b95ba79e9c607983.png" alt=""><figcaption><p>Diagram ASCII character of "S" transmitted (SPI).</p></figcaption></figure>

The clock line tells the receiving device exactly when it needs to read the data line. Two-way communication is possible, but is more complex than serial communication.

* One of the devices is labelled the controller. This is the only device allowed to send clock signals. All other devices become secondary devices that must follow the controller's clock signal to transmit data back.
* If two-way communication is used, two lines are used:
  * Peripheral-In-Controller-Out (PICO) = Communication is sent from the controller.
  * Peripheral-Out-Controller-In (POCI) = Communication is sent from the secondary device back to the controller.

The controller sends a clock signal and a command out to the device using the PICO line and keeping the clock signal, the controller receives data back on the POCI line.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/55b41ceb83ddf1ebe0fa6b89f93658f8.png" alt=""><figcaption><p>Diagram ASCII character of "S" transmitted (SPI 2-way).</p></figcaption></figure>

While there can only be one controller, there can be multiple secondary devices. To save wires and ports, all devices can use the same SCK, PICO, and POCI lines. A 4th wire called the Chip Select (CS) wire, is used to identify the device that the communication is meant for.

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/cd478aa5322feda6199648ee392f36fc.png" alt=""><figcaption><p>CS wire (4th)</p></figcaption></figure>

SPI communication is more complex than USART, but a dedicated clock line increases the speed to communicate and improves reliability.

### I2C

The Inter-Integrated Circuit (I2C) communication protocol was created to deal with the limitations of both the USART and SPI communication protocols.

* USART is asynchronous and clock built into the transmit and receive lines. Speeds are reduced to ensure reliable communication.
* SPI is faster and more reliable than USART, but it requires many more wires for communication for every additional peripheral Chip Select wire.

Similar to USART, I2C only makes use of two lines for communications. I2C uses a Serial Data (SDA) line and Serial Clock (SCL) line for communication.

* I2C uses an Address signal that is sent on the SDA wire instead of a Chip Select wire to determine which peripheral is being communicated to.
  * The Address tells all controllers and peripherals which device is trying to communicate and to which device it is trying to communicate to.
*   Once the signal is sent, a Data signal can be used to send the actual communication. To notify other controllers and peripherals that communication is happening and prevent devices from talking over each other, A Start and Stop signal is used.

    * Each device can monitor Start and Stop signals to determine if the lines are busy with communication.

    <figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/ce2b96adbbde1dcbc69dbf29eb027733.png" alt=""><figcaption><p>I2C</p></figcaption></figure>

    Since an external clock line is used, communication is still faster and more reliable than USART, and slightly slower than SPI.

    * The use of an Address signal means up to 1008 devices can be connected to the same two lines and be able to communicate.

## Analyze the Logic

In order to analyze the logic data dump, we will need to use a logic analyzer tool called [Saleae](https://www.saleae.com/).
