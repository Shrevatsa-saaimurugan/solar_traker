# solar_traker

### 1. Libraries and Constants:

```cpp
#include <Servo.h>
#define LDR1 A0
#define LDR2 A1
#define error 10
```

- **Servo Library:** This line includes the Servo library, providing functions to control a servo motor.

- **LDR Pins and Error Threshold:** `LDR1` and `LDR2` are defined as the analog input pins for two LDR sensors. The `error` constant is set to 10, representing the threshold for considering a significant difference in LDR values.

### 2. Initialization:

```cpp
int Spoint = 90;
Servo servo;
```

- **Starting Position and Servo Object:** `Spoint` is initialized to 90, representing the starting position of the servo motor. An instance of the Servo class is created and named `servo`.

### 3. Setup Function:

```cpp
void setup() {
  servo.attach(11);
  servo.write(Spoint);
  delay(1000);
}
```

- **Servo Initialization:** The `setup` function attaches the `servo` object to digital pin 11 on the Arduino. It then sets the initial position of the servo to `Spoint` (90 degrees) and introduces a delay of 1000 milliseconds (1 second).

### 4. Loop Function:

```cpp
void loop() {
  int ldr1 = analogRead(LDR1);
  int ldr2 = analogRead(LDR2);

  int value1 = abs(ldr1 - ldr2);
  int value2 = abs(ldr2 - ldr1);

  if ((value1 <= error) || (value2 <= error)) {
    // No significant difference, do nothing
  } else {
    if (ldr1 > ldr2) {
      Spoint = --Spoint;
    }
    if (ldr1 < ldr2) {
      Spoint = ++Spoint;
    }
  }

  servo.write(Spoint);
  delay(80);
}
```

- **LDR Readings and Difference Calculation:**
  - `ldr1` and `ldr2` store the analog readings from LDR1 and LDR2, respectively.
  - `value1` and `value2` calculate the absolute differences between the LDR readings.

- **Error Check and Servo Adjustment:**
  - If the differences are within the defined `error` threshold, no significant adjustment is made.
  - Otherwise, the code compares the LDR readings to determine in which direction the light intensity is higher.
  - Depending on the comparison, it increments or decrements the `Spoint` value, adjusting the servo position.

- **Servo Movement and Delay:**
  - The new servo position (`Spoint`) is written to the servo motor.
  - An 80 milliseconds delay is introduced before the next iteration of the loop.

### Hardware Setup:

- Connect the LDR sensors to the defined pins (A0 and A1).
- Connect the servo motor to digital pin 11 on the Arduino.

### Adjustments:

- Calibration may be required based on your specific hardware and environmental conditions.
- Fine-tune the `error` threshold and delay values for optimal performance.

This code essentially creates a simple solar tracking system that adjusts the position of a solar panel or collector to maximize exposure to light sources.
