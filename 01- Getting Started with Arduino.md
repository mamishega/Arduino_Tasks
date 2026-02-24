# Getting Started with Arduino

## What is Arduino?

Arduino is an open-source ecosystem designed to make electronics and physical computing accessible to everyone from students and hobbyists to professional engineers.
Think of it as the "brain" for a DIY project. It allows you to write code that interacts with the physical world through sensors, motors, and lights.

### Why Arduino?

**Easy to learn** - Beginner-friendly syntax  
**Open source** - Free software and hardware designs  
**Cross-platform** - Works on Windows, macOS, Linux  
**Inexpensive** - Boards start at $5-$25  
**Extensible** - Thousands of libraries available

**1. The Three Pillars of Arduino**
Arduino isn't just a piece of hardware; it’s a combination of three distinct components:

- **The Hardware (Microcontroller Boards):** These are the physical circuit boards. The most famous is the Arduino Uno, but there are dozens of others (Nano, Mega, ESP32-based versions) designed for different sizes and power needs.
- **The Software (Arduino IDE):** A free program you download on your computer. This is where you write your instructions (called Sketches) and "upload" them to the board via a USB cable.
- **The Language:** Arduino uses a simplified version of C/C++. It is designed to be human-readable, using straightforward commands like `digitalWrite(13, HIGH)`; to turn on a light.

**2. How It Works: Input & Output**
Arduino follows a simple logic cycle: Input → Process → Output.

| Component  | Function                                | Examples                                                              |
| ---------- | --------------------------------------- | --------------------------------------------------------------------- |
| Input      | Sensors that "feel" the world           | Buttons, Temperature sensors, Motion detectors, Light sensors         |
| Processing | The Arduino "thinks" based on your code | "If the button is pressed..." or "If the tempreature gets too hot..." |
| Outputs    | Actions the Arduino takes               | Turning on an LED, spinning a motor, displaying text on a screen      |

**3. Why is it so popular in education?**
Arduino stands out for a few specific reasons:

- **Standardization:** Because it is open-source, thousands of "libraries" (pre-written code) exist. If you want to use a specific sensor, someone has likely already written the code for it.

- **Durability:** The boards are relatively "hard to kill," making them perfect for classroom environments.

- **Cross-Platform:** It works perfectly on Windows, macOS, and Linux (and even via web editors like Wokwi).

## Variable

A variable is a named container used to store a piece of information in the board's memory. Think of it like a labeled box where you can put a number or a character, and then change that value whenever the program needs to.

Unlike Python, where variables are flexible and automatically adapt to the type of data you assign, Arduino C requires you to explicitly declare the data type before using the variable.

**1. Creating a variable**

To create a variable, you must follow this syntax:

`int         ledPin       = 13;`

`data_type  VariableName  = Value;`

- **Data Type:** What kind of data is it? (Whole number? Decimal? Text?)

- **Name:** What will you call it? (e.g., ledPin, sensorValue)

- **Value:** What is the starting data?

- **Semicolon (;):** The "period" at the end of every C++ sentence

**2. Common Data Types in Arduino**

Because Microcontrollers boards have very limited memory, choosing the right "box" size is important.

| Data Type | What it Stores           | Range / Example                     |
| --------- | ------------------------ | ----------------------------------- |
| `int`     | Whole numbers (Integers) | -32,768 to 32,767                   |
| `float`   | Numbers with decimals    | `3.14`, `25.5 `                     |
| `bool`    | True or False            | `true` or `false` (1 or 0)`         |
| `char`    | A single character       | `'A'`,`'z'` (uses single quotes)    |
| `long`    | Very large whole numbers | Used for `millis()` (time tracking) |

**3. Variable Scope**

**Global Variables:** Declared at the very top of your code (outside `setup` and `loop`). Every part of your program can see and use these. Great for pin numbers.

**Local Variables:** Declared inside a specific function (like inside `loop`). Only that function can see it. Once the function finishes, the variable is "thrown away."

## Const Qualifier

The `const` qualifier is short for "constant." When you add it to a variable declaration, you are telling the Arduino: **"This value is permanent. Do not let any part of the program change it."**

**Example:-** `const int ledPin = 13; // TheThe LED is on Pin 13 and will NEVER move`

**Why use `const` instead of a regular variable**

|                |                                      |                                              |
| -------------- | ------------------------------------ | -------------------------------------------- |
| **Feature**    | Regular Variable (`int x = 5;`)      | Constant (`const int x = 5;`)                |
| **Changeable** | Yes, anytime.                        | No, it's "locked."                           |
| **Safety**     | High risk of accidental overwriting. | Low risk; protects pin assignments.          |
| **Memory**     | Stored in RAM (precious space).      | Often optimized by the compiler to save RAM. |

**When should we use `const`?**

We use when we create/declare a :

- **Pin Numbers:** `const int sensorPin = A0;`
- **Thresholds:** `const int heatLimit = 30;`
- **Device IDs:** `const int deviceID = 101;`

**Visualising `const` in Memory**

When you use a normal variable, the Arduino sets aside a spot in **SRAM** (the active, "working" memory) because it expects the value to change. When you use `const`, the compiler can often keep that value in **Flash Memory** (where the program is stored), leaving more SRAM free for complex tasks like processing WiFi data or sensor arrays.

### Variable Example

```c++
// Declare an integer variable to store the LED GPIO pin number
int ledPin = 15;

void setup() {
  // Set the LED pin as an OUTPUT so the ESP32 can control it
  pinMode(ledPin, OUTPUT);

  // Start Serial communication at 115200 baud rate
 Serial.begin(115200);

}

void loop() {
  // Turn the LED ON
  digitalWrite(ledPin, HIGH);

  // Print LED status to Serial Monitor
  Serial.println("LED is ON");

  // Wait for 1 second
  delay(1000);

  digitalWrite(ledPin, LOW);

  // Print LED status to Serial Monitor
  Serial.println("LED is OFF");

   // Wait for 1/2 second
  delay(500);

}


```

**Use this Wokwi to test the code above** https://wokwi.com/projects/455599175951243265
