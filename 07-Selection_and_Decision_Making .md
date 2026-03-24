### 3. `Nested if`

A nested `if` is a decision inside a decision. The inner code is "protected" by the outer condition.

```c++

if (buttonState == LOW) {
  if (digitalRead(LED_PIN) == LOW) {
    digitalWrite(LED_PIN, HIGH);
  } else {
    digitalWrite(LED_PIN, LOW);
  }
}

```

## Example :
 Toggle an LED on/off with a button press. The first `if` checks if the button is pressed, and the nested `if` toggles the LED state.

**Use Wokwi to test your code : https://wokwi.com/projects/457973439550978049**

```c++
// Define pin numbers
const int LED_PIN = 2;      
const int BUTTON_PIN = 18;  

void setup() {

  // Set LED as OUTPUT
  pinMode(LED_PIN, OUTPUT);

  // Set button as INPUT with internal pull-up resistor
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {

  // Read button state
  int buttonState = digitalRead(BUTTON_PIN);

  // First IF: check if button is pressed
  if (buttonState == LOW) {

    // Nested IF: check LED state
    if (digitalRead(LED_PIN) == LOW) {
      digitalWrite(LED_PIN, HIGH);  // Turn LED ON
    }
    else {
      digitalWrite(LED_PIN, LOW);   // Turn LED OFF
    }

    delay(300); // small delay to prevent multiple presses
  }

}
```


### 4. `switch ... case`

When you have a single variable (like `mode` or `state`) that can be several specific numbers, `switch` is cleaner and faster than a long list of `if` statements.


**Switch ... case Syntax:**
```c++
switch (variable) {

  case value1:
    // code to run if variable == value1
    break;

  case value2:
    // code to run if variable == value2
    break;

  case value3:
    // code to run if variable == value3
    break;

  default:
    // code to run if none of the cases match
    break;

}

```

## Example:
  Create a simple mode selector with a button. Each press changes the mode, and the LED behaves differently based on the current mode.

**Use Wokwi to test your code : https://wokwi.com/projects/457974868693254145**
```c++
// Define pin numbers
const int LED_PIN = 2;
const int BUTTON_PIN = 18;

// Variable to store the current mode
int mode = 0;

void setup() {

  // Set LED as output
  pinMode(LED_PIN, OUTPUT);

  // Set button as input with internal pull-up
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {

  // Check if button is pressed
  if (digitalRead(BUTTON_PIN) == LOW) {

    mode++;        // change mode
    delay(300);    // debounce delay

    if (mode > 2) {
      mode = 0;    // reset mode
    }
  }

  // Use switch to control LED behaviour
  switch (mode) {

    case 0:
      // Mode 0 → LED OFF
      digitalWrite(LED_PIN, LOW);
      break;

    case 1:
      // Mode 1 → LED ON
      digitalWrite(LED_PIN, HIGH);
      break;

    case 2:
      // Mode 2 → LED BLINK
      digitalWrite(LED_PIN, HIGH);
      delay(500);
      digitalWrite(LED_PIN, LOW);
      delay(500);
      break;

    default:
      digitalWrite(LED_PIN, LOW);
      break;
  }
}
```
---

## Tips 

**1.  The “Break” Rule**

In a `switch` statement, each `case` should normally end with a `break;`     statement.

The `break;` tells the program to stop executing the current case and exit the `switch` block.

If you forget to include `break;`, the program will continue running the code in the next case as well. This behaviour is called fall-through, and it can cause unexpected results in your program.

## Example of a `switch` statement:
```c++
switch(mode){

  case 1:
    Serial.println("Mode 1");
    break;

  case 2:
    Serial.println("Mode 2");
    break;

}
```
Without `break;`, the program may run multiple cases instead of just one.

**2. Use Proper Indentation**

Although the Arduino compiler does not require spaces or indentation, good formatting is very important for humans reading the code.

Proper indentation helps you to:

- Clearly see the program structure
- Understand nested `if` statements
- Debug errors more easily
- Make your code easier for others to read and maintain

**Example of good indentation:**

```c++
if (buttonPressed) {

  if (mode == 1) {
    digitalWrite(LED, HIGH);
  } 
  else {
    digitalWrite(LED, LOW);
  }

}
```




