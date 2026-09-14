# ESP32 7-Segment Counter

A simple **ESP32-based digital counter** developed using **MicroPython**. The project uses a common-cathode 7-segment display and two push buttons to increment and decrement a number between **0 and 9**.

## 📌 Project Overview

This project demonstrates how to interface a **7-segment display and push buttons with an ESP32** using MicroPython.

The **UP button** increases the displayed number, while the **DOWN button** decreases it. The counter automatically wraps around from **9 → 0** and **0 → 9**.

## ✨ Features

* ESP32-based embedded system
* Programmed using MicroPython
* 7-segment display for number visualization
* UP push button for incrementing the counter
* DOWN push button for decrementing the counter
* Counter range from 0 to 9
* Automatic rollover from 9 to 0
* Automatic rollover from 0 to 9
* Internal pull-up resistors used for push buttons
* Simple and beginner-friendly implementation

## 🛠️ Components Required

* ESP32 Development Board
* Common Cathode 7-Segment Display
* 2 × Push Buttons
* 7 × 220Ω/330Ω Resistors
* Breadboard
* Jumper Wires
* USB Cable

## 🔌 Pin Connections

### 7-Segment Display

| Segment        | ESP32 GPIO |
| -------------- | ---------: |
| A              |    GPIO 23 |
| B              |    GPIO 22 |
| C              |    GPIO 21 |
| D              |    GPIO 19 |
| E              |    GPIO 18 |
| F              |     GPIO 5 |
| G              |     GPIO 4 |
| Common Cathode |        GND |

### Push Buttons

| Button | ESP32 GPIO | Other Connection |
| ------ | ---------: | ---------------- |
| UP     |    GPIO 32 | GND              |
| DOWN   |    GPIO 33 | GND              |

The buttons use the ESP32's internal pull-up resistors, so external pull-up resistors are not required.

## 🔄 Working Principle

The ESP32 controls the seven segments of the display by sending HIGH or LOW signals to the corresponding GPIO pins.

Each number from 0 to 9 has a predefined segment pattern.

For example:

```text
        A
       ---
    F |   | B
       - G -
    E |   | C
       ---
        D
```

For a common-cathode display:

* `1` = Segment ON
* `0` = Segment OFF

When the UP button is pressed:

```text
0 → 1 → 2 → 3 → ... → 8 → 9 → 0
```

When the DOWN button is pressed:

```text
9 → 8 → 7 → ... → 2 → 1 → 0 → 9
```

## 💻 Software Requirements

* MicroPython
* ESP32
* Thonny IDE or another MicroPython-compatible IDE

## 📂 Project Structure

```text
ESP32-7-Segment-Counter/
│
├── main.py
├── README.md
└── circuit.png
```

## 🚀 How to Run

1. Install MicroPython firmware on the ESP32.
2. Connect the ESP32 to your computer using a USB cable.
3. Open the ESP32 in Thonny IDE.
4. Copy `main.py` to the ESP32.
5. Save the file as:

```text
main.py
```

6. Run the program.
7. The 7-segment display will initially show `0`.
8. Press the UP or DOWN buttons to change the number.

## 🧑‍💻 Main Code

```python
from machine import Pin
from time import sleep

seg_pins = [23, 22, 21, 19, 18, 5, 4]
segments = [Pin(pin, Pin.OUT) for pin in seg_pins]

UP = Pin(32, Pin.IN, Pin.PULL_UP)
DOWN = Pin(33, Pin.IN, Pin.PULL_UP)

digits = [
    [1,1,1,1,1,1,0],
    [0,1,1,0,0,0,0],
    [1,1,0,1,1,0,1],
    [1,1,1,1,0,0,1],
    [0,1,1,0,0,1,1],
    [1,0,1,1,0,1,1],
    [1,0,1,1,1,1,1],
    [1,1,1,0,0,0,0],
    [1,1,1,1,1,1,1],
    [1,1,1,1,0,1,1]
]

def display(num):
    for i in range(7):
        segments[i].value(digits[num][i])

count = 0
display(count)

while True:
    if UP.value() == 0:
        count = (count + 1) % 10
        display(count)

        while UP.value() == 0:
            sleep(0.01)

    elif DOWN.value() == 0:
        count = (count - 1) % 10
        display(count)

        while DOWN.value() == 0:
            sleep(0.01)

    sleep(0.05)
```

## 📷 Circuit Diagram

Add your circuit diagram image to the repository and name it:

```text
circuit.png
```

Then add:

```markdown
![Circuit Diagram](circuit.png)
```

## 🎯 Applications

This project can be used as a basic example for:

* Digital counters
* Embedded systems learning
* GPIO programming
* 7-segment display interfacing
* Push-button interfacing
* MicroPython projects
* ESP32 laboratory experiments

## 🔮 Future Improvements

Possible improvements include:

* Add a RESET button
* Add a buzzer for button feedback
* Add automatic counting mode
* Add a two-digit or four-digit display
* Add an LCD/OLED display
* Add EEPROM/flash storage
* Add timer-based counting
* Add a menu system using multiple buttons

## 📚 Learning Outcomes

Through this project, the following concepts are demonstrated:

* ESP32 GPIO programming
* MicroPython programming
* Digital input and output
* Push-button interfacing
* 7-segment display interfacing
* Counter logic
* Button debouncing
* Embedded system programming

## 👨‍💻 Author

**Arjun**

ESP32 | MicroPython | Embedded Systems

---

⭐ If you found this project useful, consider giving the repository a **star**!
