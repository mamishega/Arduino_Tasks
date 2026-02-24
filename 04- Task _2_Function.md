# Task 1 – Smart Event Lighting Controller

### Scenario

You have been hired to design a Smart Event Lighting Controller for a small stage performance.

The event organiser wants:

- A Welcome Flash Mode

- A Warning Blink Mode

- A Celebration Rapid Flash Mode

Instead of **writing all LED control code inside `loop()`**, you must design the system using **custom functions** to keep the program organised, reusable, and professional.

The manager specifically requested:

“Make the code modular so we can reuse the lighting effects in future projects.”

### Task Requirements

You must:

- Create at least 3 custom functions

- Use meaningful function names

- Call the functions inside loop()

- Use comments

- Use delay values passed as parameters (where required)

### Functional Requirements

1. **Welcome Mode :-** LED turns ON for 1 second and OFF for 1 second (repeat 3 times)

2. **Warning Mode:-** LED blinks quickly (200ms delay) 5 times

3. **Celebration Mode:-** LED blinks very fast (100ms delay) 10 times

**Use Wokwi to test you code** **https://wokwi.com/projects/456348137954787329**

#

# Task 2 - Emergency Signal Device Using LED

### Scenario

You are working as a junior embedded systems developer for a marine safety equipment company.

Your task is to create a simple emergency signalling device using an ESP32 and a single LED.

This device will be installed on:

- Small boats
- Emergency kits
- Remote camping gear
- Survival equipment

The device must automatically blink the SOS distress signal in Morse code, which is internationally recognised.

### System Requirements

The emergency signal must:

- Be low power
- Be simple and reliable
- Use only one LED
- Blink continuously
- Follow correct Morse timing

**Morse Code Pattern**

The device must blink:

**`S`= dot dot dot**

**`O` = dash dash dash**

**`S` = dot dot dot**

#

### Timing Requirements

#

| **Signal**               | **LED ON Time**     |
| ------------------------ | ------------------- |
| Dot                      | 0.2 seconds (200ms) |
| Dash                     | 0.6 seconds (600ms) |
| OFF between blinks       | 0.2 seconds (200ms) |
| Pause between SOS cycles | 1 second            |

#

## Programming Requirements

#

Students must:

- Create a function dot()
- Create a function dash()
- Create a function sendSOS()
- Call sendSOS() inside loop()
- Use comments

**Use Wokwi to test you code** **https://wokwi.com/projects/456349405100318721**

#

# TASK 3 – Adjustable Warning Light

### Scenario

You are working for a factory that uses LED warning indicators on machines.

Different machines require different blink speeds depending on risk level.

Your task is to create a reusable function that controls the blink speed using one parameter.

### Functional Requirements

- Create a function named `warningBlink()` with one parameter
- The parameter `speed` controls how long the LED stays ON and OFF
- Inside `loop()`, call the function with different speeds

**_Example behaviour:_**

- `warningBlink(1000);` :- Slow warning
- `warningBlink(300);` :- Medium warning
- `warningBlink(100);` :- Critical warning
- **Use Wokwi to test you code https://wokwi.com/projects/456350511330290689**

#

# TASK 4 – Smart Beacon Pattern Controller

### Scenario

You are designing a portable emergency beacon.

The client wants the LED to blink in different patterns depending on the situation.

Instead of creating many separate functions, your manager asks you to design one flexible function that accepts multiple parameters.

**Use Wokwi to test you code https://wokwi.com/projects/456350851250359297**
