

**Overview**
The Solenoid Groovebox is a standalone, electro-mechanical drum machine powered by an Arduino Nano. Unlike standard digital synthesizers, this sequencer drives physical solenoids to strike real-world objects (glass, wood, metal), creating an acoustic, organic beat. It features a fully custom non-blocking software architecture, an interactive OLED interface, and dedicated MOSFET power stages for safe hardware control.



https://github.com/user-attachments/assets/720d10ea-889f-4a5f-9baf-f02392922117



**Key Features**
•	Electro-Mechanical Percussion: 2 independent sequencer tracks (Track A & Track B) driving heavy-duty 12V solenoids.
•	Non-Blocking Architecture: Built entirely on millis() timers and hardware interrupts. The system guarantees zero latency during UI updates, rotary encoder polling, or track switching, ensuring a rock-solid musical timing.
•	Smart UI / UX: * 128x64 I2C OLED display providing real-time visual feedback.
o	Context-aware UI: the screen dynamically inverts colors (White-on-Black vs. Black-on-White) to clearly indicate whether the user is editing Track A or Track B.
o	Live playhead animation and visual beat/off-beat accents.
•	Real-Time Control: Rotary encoder for BPM adjustments (40-240 BPM) and track switching, plus a dedicated Play/Stop hardware interrupt with auto-reset.
•	Standalone Power: Completely independent from USB power, utilizing an LM2596 DC-DC buck converter to safely split a 12V battery source into a 12V power rail (for solenoids) and a 5V logic rail (for the MCU and UI).

**Hardware Components**
•	MCU: Elegoo Arduino Nano (ATmega328P)
•	Actuators: 2x JF-0530B 12V Push-Pull Solenoids
•	Power Drivers: 2x IRLZ44N Logic-Level MOSFETs (equipped with 10kΩ pull-down resistors, 220Ω gate resistors, and UF4007 flyback diodes for back-EMF protection)
•	Display: 0.96" OLED Display 128x64 (SSD1306, I2C protocol at 400kHz)
•	Controls:
o	1x Rotary Encoder with Push-Button
o	8x Tactile Push-Buttons (Step Sequencer Input)
o	1x Tactile Push-Button (Play/Stop)
•	Power Supply: 12V Battery Pack + LM2596 DC-DC Buck Converter Step-Down Module

**Pinout & Architecture**
Component	Arduino Nano Pin	Notes
Solenoid A (Gate)	D9	PWM Capable
Solenoid B (Gate)	D10	PWM Capable
Encoder CLK	D2	Hardware Interrupt (attachInterrupt)
Encoder DT	D3	Hardware Interrupt (attachInterrupt)
Encoder SW	D4	Track A/B Toggle
Step Buttons 1-8	D5 to A3	Internal Pull-ups enabled
Play/Stop Button	D12	Internal Pull-up enabled
OLED SDA / SCL	A4 / A5	I2C Bus
**Future Roadmap (WIP)**
•	Velocity / Dynamics Control: Implementing PWM (analogWrite()) on pins D9 and D10 to control the striking force of the solenoids, enabling ghost notes and dynamic accents. This will be controlled via dedicated hardware potentiometers (Pins A6/A7) or an encoder-driven software menu.
•	Acoustic Enclosure: Designing and 3D-printing a custom chassis with built-in acoustic resonators and mounts to hold the solenoids perfectly aligned with the target objects.
•	MIDI Implementation: Adding standard 5-pin MIDI IN/OUT circuitry to sync the groovebox with external DAWs (Ableton Live, Logic) or other hardware synthesizers.

