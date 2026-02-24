#

# Function

Functions are the building blocks of Arduino programming. They allow us to group lines of code together and assign a name to that group. This provides four major benefits:

- Reusability: Write code once and use it many times without retyping.

- Organisation: Break a complex project (like a Robot) into smaller, manageable pieces (like `moveForward()`, `scanSensor()`, `stop()`).

- Debugging: It is much easier to find an error in a small function than in a 200-line "wall of code."

- Modularity: Functions allow us to create Libraries—collections of code that can be shared and used across different projects.

Think of a function as a mini-program that stays "on standby" until the main program calls it into action.

#

## Calling a Function

"Calling" a function means telling the Arduino to jump to that specific group of code and execute it. You can call the same function as many times as you like.

You have already been calling built-in Arduino functions! For example:

- `pinMode(2, OUTPUT);` — You are calling a predefined function that configures hardware.

- `digitalWrite(2, HIGH);` — You are calling a function that sends voltage to a pin.

- `Serial.println("Hello");` — Just like the print function in Python, this is a built-in function that sends text to your computer screen.

### The Importance of Parentheses `()`

Notice that every function name is followed by **brackets/parentheses** `()`. This is the syntax used to call the function. These brackets act as a "mailbox" used to pass in information that the function needs to do its job.

**Example:** The `delay()` function needs to know how long to wait. We pass that information inside the brackets: `delay(1000)`;.

#

## Defining Your Own Function

In Arduino (C++), you must tell the computer what type of data the function will send back. If it sends nothing back, we use the keyword `void`.

```c++
void function_name () {
//code to be executed
}

```

The `function_name` is the name we give our function and what we use to "call" it. A function name should always describe its purpose.

**Example: Creating an Led On function**

**_Live Demo_** https://wokwi.com/projects/456345525652798465

```c++
const int ledPin = 2;

void setup() {
  pinMode(ledPin, OUTPUT);
}

// 1. DEFINING the function
// This "recipe" tells the Arduino how to turn on the LED and wait
void ledON() {
  digitalWrite(ledPin, HIGH);
  delay(1000); // Keep it on for 1 second
}


```

### Code Breakdown

- **The Header** **(`void ledON()`)**: `void` tells the Arduino this function performs a task but doesn't return a number (like a calculation would).

- The Name: `ledON` is the unique name we chose for the function.
- **The Body (`{ ... }`):** Everything inside the curly braces is what happens when the function is called.

- **The Semicolon:** Notice there is no semicolon after the function name when you are defining it, but there is a semicolon when you call it in the `loop()`.

### Calling the Function

To call the above functions, we simply use the function name followed by **brackets**:

```c++

void loop() {
  // 2. CALLING the function
  // Instead of writing digitalWrite and delay again, we just use:
  ledON();

  // Turn it off so we can see the function work again in the next loop
  digitalWrite(ledPin, LOW);
  delay(1000);
}
```

#

## Built-in Functions in Arduino

Arduino has built-in functions such as:

```c++
Serial.println();
digitalWrite();
digitalRead();
delay();
pinMode();
```

**Example:-**

```c++
 Serial.println("Hello");
```

**Code explanation**

- `Serial.println` is the function

- The brackets `() `are used to pass information

- `"Hello"` is the argumen

#

## Functions With Parameters

Functions can also take in information to make them more powerful. This is done by adding parameters to the function definition. Think of parameters as the inputs to our mini-programs.

Parameters are variables that are passed into the function when it is called. This allows us to make our functions more flexible and reusable. Instead of having a function that only does one specific thing, a parameter allows it to adapt based on what we tell it.

**The Syntax**

Arduino C++ requires you to specify the data type for each parameter:

```c++
void functionName(int parameter1, float parameter2) {
    // code to be executed using these parameters
}
```

- **Data Type:** You must state if the input is an `int`, `float`, `bool`, etc.

- **Commas:** Multiple parameters are separated by commas.

- **Usage:** You can use these parameters as variables anywhere inside the curly braces `{ }` of that function.

**Example: A Flexible LED Blink**

Instead of having a function that always waits for 1 second, we can create one where we decide the speed every time we call it.

**\* Live Demo** https://wokwi.com/projects/456346420723638273

```c++
const int ledPin = 18; // Based on your ESP32-S2 IO18 label

void setup() {
  pinMode(ledPin, OUTPUT);
}

// DEFINING the function with a parameter called 'ms'
void blinkCustom(int ms) {
  digitalWrite(ledPin, HIGH);
  delay(ms); // Uses the parameter as the delay time
  digitalWrite(ledPin, LOW);
  delay(ms);
}

void loop() {
  // CALLING the function with different values
  blinkCustom(100);  // Fast blink
  blinkCustom(1000); // Slow blink
}
```
