# Epever-XTRA-Raspi4B
This repository explain how to parse data from epever solar charge controller use Raspberry Pi 4 Model B from RS485 ModBus. This project use Node-RED, not use python. Data from solar charge controller will be parsed and send to data logger using http request.

## Register Reference
[ModBus Register Reference](https://github.com/juanpradana/Epever-XTRA-Raspi4B/blob/main/ControllerProtocolV2.3.pdf)

## Hardware
- SCC Epever Xtra
- Raspberry Pi 4 Model B
- 2 way rs-485 to TTL converter

## Diagram
- Wiring

![Diagrams](https://github.com/juanpradana/Epever-XTRA-Raspi4B/assets/30497994/a84579c5-80cb-4d8f-a062-85d8553f0c59)


- Device

![device](https://github.com/juanpradana/Epever-XTRA-Raspi4B/assets/30497994/8515a22a-21ff-4126-a87e-d094acb115cb)


## Wire
- Raspi to rs485 module

| Raspi | 2 Way RS485 to TTL |
| --- | --- |
| Pin 4 | VCC |
| Pin 6 | GND |
| Pin 10 | RX |
| Pin 8 | TX |

- rs485 module to SCC

| RS485 Module | SCC |
| --- | --- |
| A+ | Green Cable |
| B- | Blue Cable |

## Setup Device
### Setting up Raspi
[raspi setup tutorial](https://www.raspberrypi.com/documentation/computers/getting-started.html)

### Install Node-RED
[install Node-RED](https://nodered.org/docs/getting-started/raspberrypi)

### Enable Serial Port
- Open terminal ```sudo raspi-config```
- Choose __Interface Options__
- Choose __Serial Port__
- Would you like a login shell to be accessible over serial? __No__
- Would you like the serial port hardware to be enabled? __Yes__
- __Reboot__
- Open terminal ```sudo nano /boot/config.txt```, add ```dtoverlay=uart0``` under ```enable_uart=1```

  ![enable overlay](https://github.com/juanpradana/Epever-XTRA-Raspi4B/assets/30497994/41e26746-07de-4cd4-9354-eb48598af770)

  Then save exit.

### Setup node-red and Device
- Open node-red ```http://localhost:1880/```
- Install Pallete ```node-red-contrib-modbus```
- Import flow from [scc parser](https://github.com/juanpradana/Epever-XTRA-Raspi4B/blob/main/scc-parser.json) into node-red and deploy

  ![image](https://github.com/juanpradana/Epever-XTRA-Raspi4B/assets/30497994/5bd05413-254d-4c4a-9f5b-3536e633da2f)

- Assemble all the components (raspi, rs485 converter and scc)

## Result
![image](https://github.com/juanpradana/Epever-XTRA-Raspi4B/assets/30497994/5e915ba5-85c8-49a3-95e3-bca21a4b007c)
