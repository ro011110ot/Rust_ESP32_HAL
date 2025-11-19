# Button Pressed

This project demonstrates how to read a digital input from a GPIO pin, such as a button press, on an ESP32, and optionally control an LED based on the button's state.

## Functionality

The application configures GPIO0 as an input pin, typically used for the onboard "Flash" button on many ESP32 development boards. It also configures GPIO2 as an output pin to control an external LED. The program continuously monitors the state of GPIO0. When the button connected to GPIO0 is pressed (registering a LOW signal), it sets GPIO2 HIGH (turning on the LED), prints "Button Pressed" to the serial console, and introduces a small delay for debouncing to prevent multiple detections from a single press. When the button is released, GPIO2 is set LOW (turning off the LED).

## How to Run

1.  Ensure your development environment is set up as described in the [root README.md](../README.md). This includes `espup` and the necessary toolchains.
2.  Connect your ESP32 board to your computer.
3.  **Hardware Setup**:
    *   **Button**: The example typically uses the onboard "Flash" button (connected to GPIO0). If using an external button, connect it to GPIO0 and configure it as an input with a pull-up resistor (or use the internal pull-up).
    *   **LED**: Connect an LED (with a current-limiting resistor) to GPIO2.
4.  Navigate to this project's directory:
    ```bash
    cd button_pressed
    ```
5.  Build, flash, and monitor the serial output using `cargo run`:
    ```bash
    cargo run --release
    ```
    This command will compile the application, flash it to your ESP32, and open a serial monitor to display messages when the button is pressed.

## Code Example

The core logic for this example is typically found in `src/bin/main.rs`:

```rust
#![no_std]
#![no_main]

use esp_backtrace as _;
use esp_hal::{
    clock::CpuClock,
    delay::Delay,
    gpio::{Io, Output, Pull, PushPull},
    main,
    peripherals::Peripherals,
};
use esp_println::println;
esp_bootloader_esp_idf::esp_app_desc!();

#[main]
fn main() -> ! {
    let peripherals = Peripherals::take();
    let io = Io::new(peripherals.GPIO, peripherals.IO_MUX);

    // Configure GPIO0 as input with internal pull-up for the button
    let button = io.pins.gpio0.into_pull_up_input();
    // Configure GPIO2 as output for the LED
    let mut led = io.pins.gpio2.into_push_pull_output();

    let delay = Delay::new();

    loop {
        if button.is_low().unwrap() { // Button is pressed when input is LOW
            led.set_high().unwrap(); // Turn LED on
            println!("Button Pressed");
            delay.delay_millis(50); // Debounce delay
        } else {
            led.set_low().unwrap(); // Turn LED off
        }
    }
}
```
**Note:** The specific GPIO pins (e.g., `gpio0`, `gpio2`) might need to be adjusted based on your ESP32 board and wiring.