# Selection and Decision Making in Arduino

Selection is the "brain" of your code. It allows the Microcontroller to evaluate information and choose a path. In the world of IT and IoT, every automated system—from a smart thermostat to a factory robot relies on these decision-making structures.

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
if (digitalRead(18) == LOW) {
  digitalWrite(2, HIGH); // LED ON
} else {
  digitalWrite(2, LOW);  // LED OFF
}

```

### 2. `if ... else if ... else`

Use this for "Step-based" logic. The Arduino checks from top to bottom and **stops** as soon as it finds a true condition.

```c++
int sensorValue = analogRead(34);

if (sensorValue > 3000) {
  Serial.println("Critical!");
} else if (sensorValue > 1500) {
  Serial.println("Warning");
} else {
  Serial.println("Normal");
}

```

## Tips

1. **Equality vs. Assignment:** \* `x = 10` sets x to 10.

- `x == 10` asks "is x equal to 10?"
- **Common Bug:** Putting `if (x = 10)` will always return true and change your variable!

### Practice Challenge

**The Intelligent Streetlight:** Write a program that uses an LDR (Light Sensor) and a Button.

- **Selection 1:** If it is dark (Sensor < 500), turn the LED on.
- **Selection 2:** If it is light, the LED should stay off **UNLESS** the button is pressed (Manual Override).


