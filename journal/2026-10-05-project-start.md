# NAPO — Lesson Report
## Lesson Information
- **Lesson:** L01 — What Is a Microcontroller?
- **Date:** 2026-10-05
- **Version:** V0.1
- **Status:** Completed

---

## 1. Goal
Understand what a microcontroller is, what role it plays within an embedded system, and what role the ESP32 will play within NAPO.

---

## 2. Context
NAPO must progressively become a physical system capable of receiving inputs, processing them, and producing outputs through displays, sensors, audio, and other devices.
In order to build NAPO, it is therefore necessary to first understand the component that will act as the system's main processing unit: the microcontroller.

---

## 3. Concepts Learned
### Microcontroller
A microcontroller is a small integrated circuit designed to directly control an electronic system and interact with the physical world.
Conceptually, it is a compact computer specialized for embedded systems.

### PC vs Microcontroller
A general-purpose PC is designed to run many different types of applications.
A microcontroller is designed to be embedded into a device and directly control hardware functions.

### Input → Processing → Output
An embedded system can initially be represented as:
```text
INPUT
  ↓
PROCESSING
  ↓
OUTPUT
```

The input can come, for example, from a button or a sensor.
The microcontroller reads and processes the information.
The output can be produced through a display, an LED, a motor, a speaker, or another device.

### ESP32
The ESP32 will act as the main processing and control unit of NAPO. It can be considered the 'brain' of the system at a conceptual level.
However, it does not represent the entire NAPO system: NAPO will also include external hardware and several software layers.

### Architecture
The following conceptual separation was introduced:
```text
Brain
  ↓
Behavior / Expression System
  ↓
Face Renderer
  ↓
Display
```
Each layer has a different responsibility.
The behavior system does not necessarily need to know how individual pixels are transferred to the display.

## 4. What I Did
I analyzed the following behavior:
When a button is pressed, NAPO closes its eyes for 500 ms and then opens them again.
The behavior was divided into:

### Input
```Button```
### Processing
```text
Read the button
Check its state
Decide the behavior
```
### Output
```Eyes open / Eyes closed```

The behavior was also divided into:
- Input state
- System state

## 5. Experiment
### Question
How can a simple NAPO behavior be represented without writing code?

### Setup
Conceptual system composed of:
- Button
- ESP32
- Display

### Procedure
1. Identify the input.
2. Determine the required processing.
3. Determine the output.
4. Identify the states of the behavior.
5. Identify the transitions between the states.

### Expected Result
When the button is pressed:
```text
EYES OPEN
     ↓
EYES CLOSED
     ↓
   500 ms
     ↓
EYES OPEN
```

### Actual Result
The behavior was correctly modeled at a conceptual level.
The difference between the button state and the NAPO behavior state was also recognized.

## 6. Problems
### Initial Problem
Initially, the identified states were:
```text
pressed
not pressed
```
However, these represent the states of the button, not the states of NAPO's behavior.

## 7. Investigation
### Distinction Between Input State and System State
The following distinction was introduced:
```text
Input state:
BUTTON = PRESSED

System state:
NAPO = EYES CLOSED
```
This leads to the more general concept of internal system state and prepares for the introduction of state machines.

## 8. Solution
### The behavior was represented as:
```text
EYES OPEN
     │
     │ button pressed
     ▼
EYES CLOSED
     │
     │ 500 ms
     ▼
EYES OPEN
```
### 9. What I Learned
I learned that a microcontroller is an embedded computer designed to interact directly with physical systems.
I understood the model:
```text 
Input → Processing → Output
```
I understood that the ESP32 will be a central component of NAPO, but that it is not the entire system.
I also started distinguishing between:
```text
input
input state
system state
event
output
```

### 10. Important Technical Details
The microcontroller acts as the connection between software and the physical world.
We also introduced the concept of firmware: software running directly on the microcontroller.
NAPO's architecture should maintain a separation between behavior and graphical rendering.

## 11. Mistakes and Misconceptions
### Initial Mistake
Considering:
```PRESSED / NOT PRESSED```
to be NAPO's states.

### Correction
These are the states of the input.
The behavior states can instead be:
```text
EYES OPEN
EYES CLOSED
```
with a timed transition between them.
