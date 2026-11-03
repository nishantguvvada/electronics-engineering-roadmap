# Electronics + Raspberry Pi: a practical beginner roadmap

This is a hands-on path for learning how software controls real hardware. It starts with safe, low-voltage circuits and Raspberry Pi GPIO, then moves through sensors, data logging, displays, and properly driven actuators.

## What you are learning

You are not only learning to "use a Raspberry Pi." You are learning four connected skills:

1. **Electronics basics:** voltage, current, resistance, polarity, grounds, breadboards, and measuring circuits.
2. **Programming hardware:** Python, GPIO inputs/outputs, timing, state, errors, and logging.
3. **Interfaces:** digital GPIO, PWM, I²C, SPI, UART, and later analog-to-digital conversion.
4. **Engineering practice:** read pinouts and datasheets, test one change at a time, measure before powering on, document wiring, and design for safe failure.

## The right board for the job

Start with a **full Raspberry Pi**—a Pi 4 or Pi 5—for this roadmap. It runs Linux, Python, networking, a camera, and local web dashboards. Its 40-pin header makes it excellent for learning GPIO and building connected projects.

Also plan to buy a **Raspberry Pi Pico or Pico W** after Projects 1–5. A Pico is a microcontroller rather than a Linux computer. It is better for learning analog inputs, precise timing, low-power projects, and embedded-style control. This is an addition, not a replacement: using both teaches you when to choose a computer versus a microcontroller.

> **Important:** Raspberry Pi GPIO uses **3.3 V logic**. Do not put 5 V on a GPIO pin. GPIO pins are signal pins, not a power source for motors, relays, heaters, LED strips, or other significant loads. Use a driver board/transistor/MOSFET and an appropriately rated external supply for those loads.[2]

---

## Buy once: starter hardware

Buy only the essentials first. Add modules when a project needs them.

### Core Raspberry Pi kit

- Raspberry Pi 4 (2–4 GB RAM is enough) or Raspberry Pi 5
- Official, correctly rated USB-C power supply for the exact Pi model
- 32 GB or larger quality microSD card
- Case with cooling appropriate to the board
- Micro-HDMI-to-HDMI cable and monitor/keyboard/mouse **or** a reliable SSH setup
- 40-pin GPIO header already fitted (normally present on full-size Pi boards)

### Breadboard and measurement kit

- Full-size solderless breadboard
- Male-to-male jumper-wire assortment
- Male-to-female and female-to-female jumper wires
- Basic digital multimeter with voltage, resistance, and continuity modes
- LED assortment
- Resistor kit; at minimum: 220 Ω, 330 Ω, 1 kΩ, 4.7 kΩ, and 10 kΩ
- Tactile pushbuttons (at least 4)
- Small piezo buzzer, preferably a low-voltage passive buzzer
- Wire cutters/strippers and a notebook or wiring-photo habit

### Add later, only when needed

- BME280 or AHT20 **3.3 V-compatible I²C** temperature/humidity/pressure sensor
- Small I²C OLED display (commonly 128×64)
- Raspberry Pi Camera Module and the correct cable for your Pi model
- PIR motion sensor rated for safe low-voltage use
- Raspberry Pi Pico/Pico W with headers and micro-USB cable
- MCP3008 ADC (analog-to-digital converter) and 10 kΩ potentiometer
- Small hobby servo **plus a separate regulated 5 V supply**
- H-bridge motor-driver board and a small DC motor, for later experiments

Do **not** start with mains electricity, high-current batteries, household appliances, exposed relays, chargers, heaters, or a motor wired directly to a GPIO pin. Start with isolated low-voltage DC projects only.

---

## Roadmap

### Stage 0 — Setup and safe habits (1–2 days)

1. Install Raspberry Pi OS with Raspberry Pi Imager and boot the Pi.[1]
2. Learn Terminal basics: `pwd`, `ls`, `cd`, `mkdir`, `python`, `pip`, and editing a file.
3. Write and run a Python `print("hello")` script.
4. Learn the difference between **physical pin numbers** and **BCM GPIO numbers**. Run `pinout` on the Pi before wiring.
5. With the Pi powered off, learn breadboard rails and rows. Use the multimeter's continuity mode to confirm what is connected.[4]

**Exit criterion:** you can boot the Pi, SSH or use its desktop, identify ground/3.3 V/GPIO pins, and make a small Python program run.

### Stage 1 — First circuits and GPIO (1–2 weeks)

Learn voltage, current, resistance, polarity, Ohm's law, LEDs, buttons, pull-up/pull-down resistors, and safe GPIO. Use `gpiozero` recipes as the current Python reference.[3]

**Exit criterion:** you can wire and explain an LED with a resistor, read a button reliably, and debug a non-working circuit with a multimeter.

### Stage 2 — Timing, state, and outputs (1–2 weeks)

Learn loops, event callbacks, software debounce, PWM (fast on/off switching used to vary average power), small state machines, and basic program structure.

**Exit criterion:** you can build an interactive device that responds predictably to a button or sensor.

### Stage 3 — Sensors and buses (2–3 weeks)

Learn I²C first: SDA/SCL lines, device addresses, enabling I²C, and using `i2cdetect` before debugging Python. Use sensor breakout boards designed for 3.3 V systems. Adafruit's Raspberry Pi I²C guide is a useful setup reference.[5]

Then learn SPI and UART through one small experiment each. Do not try to learn all buses in one project.

**Exit criterion:** you can verify a sensor is visible on its bus, read it, handle a missing device, and explain its measurement limits.

### Stage 4 — Store and display data (2 weeks)

Timestamp readings to CSV or SQLite; graph them; build a small local dashboard; use a display or LEDs as local feedback. This is where your software background becomes useful.

**Exit criterion:** you have a sensor project that survives a restart, stores readable data, and shows useful status.

### Stage 5 — Cameras, networking, and reliability (2–3 weeks)

Add a camera, local network API, simple web UI, system logs, automatic startup with `systemd`, and graceful shutdown/recovery.

**Exit criterion:** you can deploy a project that starts after reboot and can be diagnosed from logs.

### Stage 6 — Microcontrollers and actuators (ongoing)

Use a Pico/Pico W to learn ADC, PWM, serial debugging, interrupts, and low-power operation. For motors/servos, learn drivers, external supplies, common grounds, current budgets, and flyback protection before building anything mechanical.

**Exit criterion:** you can explain why an actuator needs a driver and separate power, not just make it move once.

---

## The first 10 projects

Build these **in order**. Do not advance until the current project works and you can explain each wire.

### 1. Blink an LED

**Build:** blink one LED at different rates with Python and `gpiozero`.

**Hardware to purchase/use:**

- Raspberry Pi setup from the core kit
- Solderless breadboard
- 1 LED
- 1 × 220–1 kΩ resistor
- 2–3 male-to-male jumper wires

**Learn:** LED polarity, current-limiting resistors, GPIO output, timing, BCM pin numbers.

**Done when:** you can change the blink pattern and draw the circuit from memory.

### 2. Button-controlled LED

**Build:** press a button to turn on an LED; then switch to event-driven code.

**Hardware to purchase/use:**

- Project 1 hardware
- 1 tactile pushbutton
- 2–3 additional jumper wires
- Optional: 10 kΩ resistor if you build an external pull-up/pull-down version

**Learn:** GPIO input, pull-up/pull-down resistors, floating inputs, event callbacks, debouncing.

**Done when:** the LED responds once per press without false presses.

### 3. Reaction-time game

**Build:** an LED turns on after a random wait; the player presses a button as quickly as possible; Python records the time and best score.

**Hardware to purchase/use:**

- Project 2 hardware
- Optional: second button for reset
- Optional: low-voltage piezo buzzer

**Learn:** program state, random timing, timestamps, input events, simple user interaction.

**Done when:** you can save high scores to a small local file.

### 4. PWM night-light / dimmer

**Build:** fade an LED with PWM. Optional extension: use a potentiometer to control brightness.

**Hardware to purchase/use:**

- 1 LED
- 1 × 220–1 kΩ resistor
- Jumper wires and breadboard
- **For potentiometer control:** MCP3008 ADC, 10 kΩ potentiometer, and extra jumper wires

**Learn:** PWM, duty cycle, why a normal Raspberry Pi has no analog input, and why an ADC is needed for a potentiometer.

**Done when:** you can explain the difference between a digital GPIO read and an ADC measurement.

### 5. Traffic light with pedestrian button

**Build:** a red/yellow/green LED traffic light with a button-driven pedestrian sequence.

**Hardware to purchase/use:**

- 3 LEDs: red, yellow, green
- 3 × 220–1 kΩ resistors
- 1 tactile pushbutton
- Breadboard and jumper wires

**Learn:** multi-output control, finite-state machines, timed transitions, debouncing, and clear code organization.

**Done when:** the pedestrian request waits for a safe state instead of interrupting any point in the sequence.

### 6. Electronic dice

**Build:** press a button to animate and stop on a random die roll using seven LEDs.

**Hardware to purchase/use:**

- 7 LEDs
- 7 × 220–1 kΩ resistors
- 1 tactile pushbutton
- Breadboard and jumper wires
- Optional later extension: 74HC595 shift register and additional resistors/wires

**Learn:** arrays/lists, reusable functions, random numbers, output mapping, and conserving GPIO pins with a shift register.

**Done when:** each number from 1–6 has the correct pip pattern.

### 7. Raspberry Pi CPU-temperature status bar

**Build:** display the Pi's own CPU temperature on three to eight LEDs.

**Hardware to purchase/use:**

- 3–8 LEDs
- Matching 3–8 × 220–1 kΩ resistors
- Breadboard and jumper wires

**Learn:** reading system information, thresholds, polling, status feedback, and avoiding repeated hard-coded logic.

**Done when:** your program logs thresholds crossed and has a sensible update interval.

### 8. Environmental monitor and logger

**Build:** read temperature/humidity/pressure from an I²C sensor, show it on the terminal or OLED, and log values to CSV/SQLite.

**Hardware to purchase/use:**

- BME280 or AHT20 I²C sensor breakout compatible with 3.3 V logic
- Female-to-female jumper wires **or** a compatible STEMMA QT/Qwiic breakout and cable
- Optional I²C OLED display
- Optional enclosure after the prototype works

**Learn:** I²C, device addresses, Linux bus scanning, sensor libraries, timestamped data, calibration/placement limits, and error handling.

**Done when:** the project handles a disconnected sensor gracefully and graphs at least one day of readings.

### 9. Motion-triggered camera/logger

**Build:** detect motion, capture an image, timestamp it, and record the event. Add a simple web page later if desired.

**Hardware to purchase/use:**

- Raspberry Pi Camera Module
- Correct camera ribbon cable for your exact Pi model
- PIR motion sensor suitable for a 3.3 V GPIO interface (check its module documentation)
- Breadboard/jumpers
- Optional status LED plus 220–1 kΩ resistor
- Optional larger microSD card for image storage

**Learn:** camera interfaces, filesystem organization, timestamps, sensor-triggered code, storage management, and privacy-by-design.

**Done when:** the camera captures only after a valid event and old files are managed safely.

> Use this only where everyone recorded has consented. Do not point it at neighbors, public spaces, or private areas without permission.

### 10. Properly powered servo controller

**Build:** control a small hobby servo from a button, sensor, or web UI. This is the first actuator project because it forces you to learn power separation.

**Hardware to purchase/use:**

- Small hobby servo
- **Separate regulated 5 V supply** rated for the servo's expected current
- Suitable connector/wires; do not rely on the Pi's GPIO power pin
- Breadboard/jumpers for signal only
- Optional button or sensor from earlier projects
- Optional 470–1000 µF electrolytic capacitor near the servo supply if recommended by the chosen servo/driver documentation

**Learn:** PWM control signals, current spikes, shared ground where the setup requires it, power budgets, and debugging brownouts.

**Safety rule:** connect the Pi GPIO only to the servo's control signal. Power the servo from its own supply. Follow the servo documentation for common-ground wiring. Never connect a motor directly to a Pi GPIO pin.

**Done when:** the Pi stays stable while the servo moves, and you can explain the entire power path.

---

## Tutorials and videos: watch in this order

Do not binge-watch. Watch one lesson, build its circuit, change one variable, break it safely, then fix it.

1. **Afrotechmods — [Basic Electricity: Resistance and Ohm's Law](https://www.youtube.com/watch?v=NfcgA1axPLo)**
   - Watch before Project 1.
   - Covers voltage, current, resistance, Ohm's law, LEDs, and current limiting.[10]

2. **Official Raspberry Pi — [Getting started documentation](https://www.raspberrypi.com/documentation/computers/getting-started.html)**
   - Use this as the current source of truth for Raspberry Pi Imager, Raspberry Pi OS, first boot, and headless setup.[1]

3. **Paul McWhorter — [Free Raspberry Pi Tutorials for Absolute Beginners playlist](https://www.youtube.com/watch?v=1WDagiA8fdU&list=PLGs0VKk2DiYxdMjCJmcP6jt4Yw6OHK85O)**
   - Main sequential course: setup, Python, Linux, GPIO, breadboarding, components, displays, sensors, and projects.[8]
   - Follow early lessons in sequence; cross-check package/UI steps against current official documentation.

4. **DroneBot Workshop — [Raspberry Pi GPIO: Getting Started with gpiozero](https://www.youtube.com/watch?v=iL_oZGHLHvU)**
   - Watch before Projects 1–3.
   - Covers GPIO header orientation, physical vs BCM numbering, 3.3 V logic, LEDs, buttons, PWM, and `gpiozero`.[9]

5. **gpiozero — [Basic Recipes](https://gpiozero.readthedocs.io/en/stable/recipes.html)**
   - Keep open while building every GPIO project. It contains small, maintained examples for LEDs, buttons, PWM, motion, distance, and other devices.[3]

6. **ExplainingComputers — [Raspberry Pi: Using GPIO Inputs](https://www.youtube.com/watch?v=NAl-ULEattw)**
   - Watch before Project 2 or 5.
   - Focus on switches, pull-up/pull-down resistors, and input handling. The code style is older, but the electrical concepts remain useful.

7. **DroneBot Workshop — [I²C with Arduino and Raspberry Pi: Two Methods](https://www.youtube.com/watch?v=me7mhrRbspk)**
   - Watch before Project 8.
   - Covers I²C concepts, addresses, bus setup, and voltage-level considerations.

8. **Adafruit — [I²C sensors and devices on Raspberry Pi](https://learn.adafruit.com/circuitpython-on-raspberrypi-linux/i2c-sensors-and-devices)**
   - Use as the practical reference when wiring and detecting your first I²C device.[5]

---

## Community advice: useful, but verify it

Two recurring points from beginner discussions are useful:

- **Build tiny projects first.** LED → button → PWM → sensor → logger is a better learning path than buying a huge kit or attempting a finished "smart home" project first.
- **Use both a Pi and a microcontroller over time.** A full Raspberry Pi is strong for Linux, Python, cameras, networking, and dashboards. A Pico/Arduino-class microcontroller is more natural for deterministic timing, analog inputs, and low-power embedded control.

Read these as community discussion, not authoritative specifications:

- [r/AskElectronics beginner resources](https://www.reddit.com/r/AskElectronics/wiki/beginners/)
- [r/AskElectronics: essential beginner tools](https://www.reddit.com/r/AskElectronics/comments/9kch81/what_are_the_essential_tools_for_starting_out/)
- [r/embedded: Raspberry Pi or Arduino for beginner work](https://www.reddit.com/r/embedded/comments/17q0k88/should_i_start_with_an_arduino_or_raspberry_pi/)

Before wiring anything, use the board's official documentation and the component's datasheet/module documentation to check pinout, voltage, current, and logic-level compatibility.

---

## Rules that prevent most beginner damage

1. **Power off before changing wires.**
2. **Check the exact pinout each time.** Never trust memory or a tutorial for a different Pi model.
3. **Use an LED resistor every time.**
4. **Never connect 5 V to a 3.3 V GPIO input.**
5. **Do not power motors, servos, relays, or LED strips from GPIO.** Use the right driver and supply.
6. **Measure before guessing.** Check voltage and continuity with a multimeter.
7. **Document each build.** Save code, a wiring diagram/photo, a parts list, and a short README in a project folder.
8. **Change one thing at a time when debugging.** First confirm power and ground, then wiring, bus detection, code, and library versions.
9. **Do not use mains voltage as a beginner project.**
10. **Make safety and privacy part of the design, not an afterthought.**

---

## What to read after the first 10 projects

- Raspberry Pi hardware/GPIO documentation for board-specific facts and pin behavior.[2]
- SparkFun's [How to Use a Breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard/all) for breadboard topology and prototyping practice.[4]
- `gpiozero` recipes for the next device you want to connect.[3]
- Datasheets for every sensor, display, motor, and driver you buy.
- Later: digital logic, transistor/MOSFET switching, op-amps, power regulation, serial protocols, soldering, perfboard, KiCad, and PCB design.

## Sources

1. [Raspberry Pi: Getting started](https://www.raspberrypi.com/documentation/computers/getting-started.html)
2. [Raspberry Pi: computer hardware and GPIO documentation](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)
3. [gpiozero: Basic Recipes](https://gpiozero.readthedocs.io/en/stable/recipes.html)
4. [SparkFun: How to Use a Breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard/all)
5. [Adafruit: I²C sensors and devices on Raspberry Pi](https://learn.adafruit.com/circuitpython-on-raspberrypi-linux/i2c-sensors-and-devices)
6. [r/AskElectronics beginner resources](https://www.reddit.com/r/AskElectronics/wiki/beginners/)
7. [r/embedded discussion: Raspberry Pi or Arduino for a beginner](https://www.reddit.com/r/embedded/comments/17q0k88/should_i_start_with_an_arduino_or_raspberry_pi/)
8. [Paul McWhorter: Free Raspberry Pi Tutorials for Absolute Beginners](https://www.youtube.com/watch?v=1WDagiA8fdU&list=PLGs0VKk2DiYxdMjCJmcP6jt4Yw6OHK85O)
9. [DroneBot Workshop: Raspberry Pi GPIO — Getting Started with gpiozero](https://www.youtube.com/watch?v=iL_oZGHLHvU)
10. [Afrotechmods: Basic Electricity — Resistance and Ohm's Law](https://www.youtube.com/watch?v=NfcgA1axPLo)
