# RTC-Clock
Configured the built in *RTC timer* on an Arm Cortex STM32F microcontroller to display time and date, allow user to store the time in an *external EEPROM*, and set the date and time.

## Logic
- Pressing the built in user button stores the current time in the *I2C EEPROM* (only the previous two times are stored)
- Holding the built in user button for longer than 1 second displays the current date and time on the LCD
- Pressing external button one toggles displaying the previous two times stored on the LCD
- Pressing external button two allows the user to change the time and date. When first pressed, it displays the first value to be set which is Year:
  - Pressing external button one in this state allows the user to cycle through all the possible value ranges for the parameter being set (Years: 0-99 from start year)
  - Pressing external button two in this state allows the user to cycle through the paramter being set (e.g. Year -> Month)
  - Once the last value (seconds) has been set, the RTC is updated and the user returns to the initial state

## Safety
- All parameter ranges loop once the max is reached (month after Dec is Jan).
- Capped the ranges for parameters at maximum value (e.g. Year: 0-99).
- Ensured user cannot select a day which does not exist in a month (e.g. April 31st).
- Added a formula to calculate the weekday instead of letting the user select to ensure the correct weekday is set.
- Added a formula to check if the user is in a leap year and allow February 29th to be a valid selection.
