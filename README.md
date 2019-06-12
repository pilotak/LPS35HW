# Pressure sensor library for Arduino
[![Build Status](https://travis-ci.org/pilotak/LPS35HW.svg?branch=master)](https://travis-ci.org/pilotak/LPS35HW)

## Supported barometers
- **LPS35HW**
- **LPS22HB**
- **LPS33W**
- **LPS33HW**

This library works with metric units, if you need imperial please consider using [MeteoFunctions](https://github.com/pilotak/MeteoFunctions) library.

```cpp
#include <Wire.h>
#include "LPS35HW.h"
#include "MeteoFunctions.h"

LPS35HW lps;
MeteoFunctions calc;

const float above_sea = 1000;  // ft

void setup() {
    Serial.begin(9600);
    Serial.println("LPS barometer test");

    if (!lps.begin()) {
        Serial.println("Could not find a LPS barometer, check wiring!");

        while (1) {}
    }
}

void loop() {
    float pressure = lps.readPressure();
    float temp = calc.c_f(lps.readTemp());

    Serial.print("Pressure: ");
    Serial.print(calc.relativePressure_f(pressure, above_sea, temp));
    Serial.print("inHg\ttemperature: ");
    Serial.print(temp);
    Serial.println("*F\n");

    delay(1000);
}
```
