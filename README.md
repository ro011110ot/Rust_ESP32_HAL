# Rust ESP32-HAL Workspace

This workspace contains a collection of examples for the ESP32 using the `esp-hal` crate.

## Projects

*   `blinky`: A simple example that blinks an LED.
*   `button_pressed`: An example that demonstrates reading a button press.
*   `hello_world`: A classic "Hello, world!" example that prints to the console.

## Prerequisites

*   Rust (nightly toolchain)
*   Xtensa toolchain for ESP32
*   `cargo-espflash`

## Building and Flashing

To build and flash a specific project, navigate to its directory and use `cargo-espflash`:

```bash
cd blinky
cargo espflash flash --monitor
```
