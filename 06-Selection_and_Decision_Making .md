### 3. `Nested if`

A nested `if` is a decision inside a decision. The inner code is "protected" by the outer condition.

```c++
if (isPowerOn) {           // Outer Gate
  if (isButtonPressed) {   // Inner Gate
    // This only runs if BOTH are true
    runMotor();
  }
}

```

## Example Project: The Multi-Function Security Button

This code combines **Selection** and **Timing** to create a smart button for your Microcontroller.

```c++
const int LED_PIN = 2;
const int BUTTON_PIN = 18;

unsigned long pressTimer = 0;
bool active = false;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {
  bool isPressed = (digitalRead(BUTTON_PIN) == LOW);

  if (isPressed) {
    // Nested Logic: Calculate how long we've been holding
    if (pressTimer == 0) pressTimer = millis();
    unsigned long duration = millis() - pressTimer;

    if (duration > 3000) {
      // Long press: Fast strobe
      digitalWrite(LED_PIN, (millis() % 100 < 50));
    } else if (duration > 1000) {
      // Medium press: Slow blink
      digitalWrite(LED_PIN, (millis() % 1000 < 500));
    } else {
      // Short press: Solid ON
      digitalWrite(LED_PIN, HIGH);
    }
  } else {
    // Not pressed: Reset everything
    digitalWrite(LED_PIN, LOW);
    pressTimer = 0;
  }
}

```


### 4. `switch ... case`

When you have a single variable (like `mode` or `state`) that can be several specific numbers, `switch` is cleaner and faster than a long list of `if` statements.

```c++
switch (mode) {
  case 0:
    stopSystem();
    break; // Stops the code from "falling through" to case 1
  case 1:
    startSystem();
    break;
  default:
    Serial.println("Unknown Mode");
    break;
}

```

---


---

## Tips


1. **The "Break" Rule:** In a `switch` statement, if you forget the `break;`, the Arduino will execute the code for the next case as well.
2. **Indentation:** While the compiler doesn't care about spaces, humans do. Use `Ctrl+T` in the Arduino IDE to auto-format your code. Clean indentation makes nested `if` blocks much easier to debug.
