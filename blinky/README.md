# Blinky

This project is a simple "blinky" example for the ESP32. It uses the `esp-hal` crate to control a GPIO pin and blink an LED.

## Functionality

The application initializes a GPIO pin as an output and toggles it in a loop, causing an attached LED to blink.

## How to Run

1.  Make sure you have the prerequisites installed (see the root README.md).
2.  Navigate to this directory.
3.  Run `cargo espflash flash --monitor` to build, flash, and monitor the output.
