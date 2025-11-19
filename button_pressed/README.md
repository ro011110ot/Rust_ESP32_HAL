# Button Pressed

This project demonstrates how to read a digital input from a GPIO pin, such as a button press, on an ESP32.

## Functionality

The application configures a GPIO pin as an input with a pull-down resistor. It then continuously polls the pin's state and prints a message to the console when the button is pressed (i.e., the input goes high).

## How to Run

1.  Make sure you have the prerequisites installed (see the root README.md).
2.  Connect a button to a GPIO pin.
3.  Update the pin number in `src/bin/main.rs` if necessary.
4.  Navigate to this directory.
5.  Run `cargo espflash flash --monitor` to build, flash, and monitor the output.
