# Selection and Decision Making in Arduino

Selection is the "brain" of your code. It allows the Microcontroller to evaluate information and choose a path. In the world of IT and IoT, every automated system from a smart thermostat to a factory robot relies on these decision making structures.

---

## The 3 Pillars of Decision Making

Every decision your Arduino makes follows this high-speed cycle inside the `loop()` function:

1. **Observation:** Read a sensor or button (e.g., `digitalRead`).
2. **Comparison:** Compare that value to a threshold (e.g., `is temperature > 30?`).
3. **Action:** Change an output based on the result (e.g., `Turn on Fan`).

---

## Comparison & Logical Operators

To make decisions, we use "math for logic."

### 1. Comparison

These compare two values and return a **Boolean** (`true` or `false`).
| Operator | Meaning | Example |
| :--- | :--- | :--- |
| `==` | Exactly equal to | `if (mode == 1)` |
| `!=` | Not equal to | `if (user != "Admin")` |
| `>` | Greater than | `if (voltage > 3.3)` |
| `<` | Less than | `if (light < 100)` |
| `%` | Modulo (Remainder) | `if (count % 2 == 0)` (Is even?) |

### 2. Logical

These allow you to check multiple conditions at once.
| Operator | Meaning | Example |
| :--- | :--- | :--- |
| `&&` | **AND** (Both must be true) | `if (isPressed && isArmed)` |
| `||` | **OR** (Either can be true) | `if (isTooHot || isTooHumid)` |
| `!` | **NOT** (Inverts the result) | `if (!isReady)` |

---

## Understanding Button Physics: Pull-up vs. Pull-down

Before writing selection code, you must understand how the Microcontroller "sees" a button. An unconnected pin is "floating"—it picks up electrical noise and gives random `HIGH/LOW` readings.

### The Internal Pull-Up (Recommended)

Using `pinMode(pin, INPUT_PULLUP)` connects an internal resistor to 3.3V.

- **Default State:** `HIGH` (The resistor "pulls" the voltage up).
- **Pressed State:** `LOW` (The button connects the pin to Ground).
- **The Logic Gap:** Beginners often find it strange that `LOW` means "On," but this is the industry standard because it is more power-efficient.

---

## Selection Structures & Examples

### 1. Simple `if ... else`

This is a binary choice: one path or the other.

```c++
// Define pin numbers
const int ledPin = 16;   //  GPIO LED 16
const int buttonPin = 18;          // GPIO BUTTON 18 

void setup() {
  // Start serial communication for debugging
  Serial.begin(115200);

  // Set LED as OUTPUT
  pinMode(ledPin, OUTPUT);

  // Set button as INPUT with internal pull-up resistor
  pinMode(buttonPin, INPUT_PULLUP);
}

void loop() {
  // Read button state
  int buttonState = digitalRead(buttonPin);

  // Check if button is pressed (LOW because of pull-up)
  if (buttonState == LOW) {

    Serial.print("The Value of the Button is: ");
    Serial.println(buttonState);

    digitalWrite(ledPin, HIGH);  // Turn LED ON

    Serial.print("The Value of LED is: ");
    Serial.println(digitalRead(ledPin));

  } else {
    digitalWrite(ledPin, LOW);   // Turn LED OFF
  }
}

```

**Use Wokwi to test your code : https://wokwi.com/projects/456875546095269889**

### 2. `if ... else if ... else`

Use this for "Step-based" logic. The Arduino checks from top to bottom and **stops** as soon as it finds a true condition.

**Use Wokwi to test your code : https://wokwi.com/projects/457476532175028225**

```c++


// Define GPIO pin numbers
const int ledPin = 16;        // LED connected to GPIO 16
const int buttonPin = 18;     // Button connected to GPIO 18

// Variable to count how many times button is pressed
int pressCount = 0;

// Variable to store previous button state
// (Used to detect a NEW press instead of holding the button)
int lastButtonState = HIGH;

void setup() {

  // Start Serial Monitor (for debugging)
  Serial.begin(115200);

  // Set LED pin as OUTPUT
  pinMode(ledPin, OUTPUT);

  // Set button as INPUT with internal pull-up resistor
  // INPUT_PULLUP means:
  // - Button NOT pressed = HIGH
  // - Button pressed = LOW
  pinMode(buttonPin, INPUT_PULLUP);
}

void loop() {

  // Read current state of button
  int buttonState = digitalRead(buttonPin);

  // -------------------------------------------------
  // Detect a NEW button press
  // buttonState == LOW  → Button is pressed
  // lastButtonState == HIGH → It was not pressed before
  // This prevents counting while button is held down
  // -------------------------------------------------
  if (buttonState == LOW && lastButtonState == HIGH) {

    pressCount++;      // Increase press counter
    delay(200);        // Small delay for debouncing

    Serial.print("Button pressed. Count = ");
    Serial.println(pressCount);
  }

  // Update last button state for next loop
  lastButtonState = buttonState;

  // -------------------------------------------------
  // if / else if / else selection structure
  // -------------------------------------------------

  // First press → LED stays ON
  if (pressCount == 1) {

    digitalWrite(ledPin, HIGH);   // Turn LED ON
  }

  // Second press → LED blinks
  else if (pressCount == 2) {

    digitalWrite(ledPin, HIGH);   // LED ON
    delay(300);                   // Wait 300ms
    digitalWrite(ledPin, LOW);    // LED OFF
    delay(300);                   // Wait 300ms
  }

  // Any other value → LED OFF
  else {

    digitalWrite(ledPin, LOW);    // Turn LED OFF
  }

  // Reset counter after third press
  if (pressCount > 2) {

    pressCount = 0;   // Start cycle again
  }
}

```



