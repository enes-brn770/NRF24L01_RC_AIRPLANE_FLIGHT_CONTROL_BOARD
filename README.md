# ✈️ NRF24L01 RC Airplane Flight Control Board

> An Arduino Nano-based control board for an electric RC airplane, featuring NRF24L01 wireless communication and an MPU6050 motion sensor.

![Project](https://img.shields.io/badge/Project-RC%20Airplane-blue)
![MCU](https://img.shields.io/badge/MCU-Arduino%20Nano-teal)
![Wireless](https://img.shields.io/badge/Wireless-NRF24L01-orange)
![Sensor](https://img.shields.io/badge/IMU-MPU6050-green)

---

## 📌 About the Project

The **NRF24L01_RC_AIRPLANE_FLIGHT_CONTROL_BOARD** is an Arduino Nano-based PCB designed for an electric RC airplane project.

The board includes the following components and connections:

- 🧠 **Arduino Nano** — main controller
- 📡 **NRF24L01+PA+LNA** — wireless communication module
- 🧭 **MPU6050** — accelerometer and gyroscope
- ⚙️ **Four servo connectors** — for control surfaces or other mechanisms
- 🔌 **ESC connector** — electronic speed controller signal connection
- 🔋 **Buck converter connection** — for voltage regulation
- 🔔 **Buzzer** — audible alerts
- 💡 **LED** — status indication

> **Note:** A completed PCB does not automatically make the aircraft ready to fly. Firmware, the transmitter/controller, failsafe behavior, the power system, and the mechanical setup must be developed and tested separately.

---

## 🔌 Pin Connections

### 🎮 Servos and ESC

| Board Connection | Arduino Nano Pin | Description |
|---|---|---|
| SERVO1 | D3 | Servo signal output 1 |
| SERVO2 | D5 | Servo signal output 2 |
| SERVO3 | D6 | Servo signal output 3 |
| SERVO4 | D9 | Servo signal output 4 |
| ESC_PIN | D10 | ESC control signal |

### 📡 NRF24L01+PA+LNA

| NRF24L01 Pin | Arduino Nano Connection |
|---|---|
| VCC | 3.3V |
| GND | GND |
| CE | D7 |
| CSN | D8 |
| SCK | D13 |
| MOSI | D11 |
| MISO | D12 |
| IRQ | Not connected |

### 🧭 MPU6050

| MPU6050 Pin | Arduino Nano Connection |
|---|---|
| VCC | 3.3V |
| GND | GND |
| SDA | A4 |
| SCL | A5 |
| INT | D4 |

### 💡 LED and 🔔 Buzzer

| Component | Arduino Nano Pin |
|---|---|
| LED | A1 |
| Buzzer | D2 |

---

## 📦 Bill of Materials (BOM)

The following table lists the components used in the PCB design, their footprints, and quantities.

| ID | Component Name | Footprint | Quantity |
|---:|---|---|---:|
| 1 | ARDUINO_NANO | `COMM-TH_ARDUINO_NANO` | 1 |
| 2 | BUCK CONVERTER | `PWRM-TH_4P-L11.5-W6.0-P2.54_ZY0305EFM-1W` | 1 |
| 3 | BUZZER-12X9 | `BUZ-TH_BD12.0-P7.60-D0.6-FD` | 1 |
| 4 | ESC C1 | `HDR-F-2.54_1X3` | 1 |
| 5 | SERVO1 C2 | `HDR-F-2.54_1X3` | 1 |
| 6 | SERVO2 C3 | `HDR-F-2.54_1X3` | 1 |
| 7 | SERVO3 C4 | `HDR-F-2.54_1X3` | 1 |
| 8 | SERVO4 C5 | `HDR-F-2.54_1X3` | 1 |
| 9 | ESC POWER | `CONN-TH_XY301V-A-5.0-2P` | 1 |
| 10 | POWER LED | `LED-TH_BD5.0_GREEN` | 1 |
| 11 | MPU6050-TH | `COMM-TH_MPU6050-TH` | 1 |
| 12 | NRF24L01+PA+LNA | `COMM-TH_L41.0-W15.5-P2.54_NRF24L01` | 1 |
| 13 | SS-12F44-G5 | `SW-TH_SS-12F44-G5` | 1 |
| 14 | Deans Connector M | `DEANS_M` | 1 |
| 15 | 1k Resistor | `R_AXIAL-0.3` | 1 |

---

## 🔋 Power System Notes

- The design is intended to use a **3S Li-Po battery**.
- A 3S Li-Po battery has a nominal voltage of **11.1V** and a fully charged voltage of **12.6V**.
- The buck converter must be verified for the required input range and load current before it is used to supply the 5V rail.
- The **NRF24L01 must be powered from 3.3V. Do not connect its VCC pin to 5V.**
- The NRF24L01+PA+LNA version may draw more current than a standard NRF24L01 module. Verify that the 3.3V regulator can supply the required current, and place suitable decoupling capacitance close to the module.
- Calculate the current requirements of the servos and the Arduino/sensor electronics separately. Servo peak currents may exceed the capacity of the logic regulator.
- Connect signal grounds according to the power-system design, maintaining a common ground reference where required.

⚠️ **Important:** The ESC power connection and ESC signal connection are not the same. Connect the ESC's battery and motor wires according to the ESC manufacturer's instructions. The board's `ESC_PIN` connection is for the control signal only.

---

## 🛠️ Suggested Arduino Libraries

The following libraries may be used when developing the firmware:

- `RF24` — NRF24L01 wireless communication
- `Wire` — I2C communication (included with the Arduino platform)
- A compatible `MPU6050` Arduino library — sensor data acquisition

Library versions and firmware details have not been specified in this README.

---

## 🧪 Testing Checklist

Before installing the board in the aircraft, test it on the workbench:

- [ ] Inspect the PCB for soldering faults and short circuits.
- [ ] Verify battery polarity and power connector orientation.
- [ ] Measure the buck converter output with a multimeter before connecting it to the board.
- [ ] Verify that the 5V and 3.3V rails have the correct voltage.
- [ ] Confirm that the NRF24L01 is supplied with 3.3V.
- [ ] Read accelerometer and gyroscope data from the MPU6050.
- [ ] Test servo outputs with the propeller removed and the motor system disabled.
- [ ] Test the ESC signal with the propeller removed and the motor safely secured.
- [ ] Define and test the failsafe behavior for loss of transmitter or radio connection.

---

## ⚠️ Safety

- Li-Po batteries can cause fire if short-circuited, connected with reversed polarity, over-discharged, or charged incorrectly. Use a suitable Li-Po charger and follow battery safety instructions.
- Use a current-limited bench power supply for initial power-up when possible.
- Never run a motor test with the propeller installed on the workbench.
- Conduct flight tests only in a suitable open area and follow applicable local regulations and model-aircraft safety practices.
- Test radio range, interference resistance, and failsafe behavior before flight.
- This project is not a certified aviation system and does not guarantee airworthiness.

---

## 👨‍💻 Developer

**Enes Baran Doğan**

Project: **NRF24L01_RC_AIRPLANE_FLIGHT_CONTROL_BOARD**

---

⭐ If you find this project useful, consider giving the repository a star!
