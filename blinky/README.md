# Blinky

This project is a simple "blinky" example for the ESP32. It uses the `esp-hal` crate to control a GPIO pin and blink an
LED.

## Functionality

The application initializes a specific GPIO pin (e.g., GPIO8) as an output. It then enters an infinite loop, where it
continuously toggles the state of this GPIO pin (from high to low and vice versa) with a delay, causing an attached LED
to blink. The article mentions two methods for controlling the pin: explicitly setting high/low or using a `toggle()`
function. This example typically uses the `toggle()` function for simplicity.

## How to Run

1. Ensure your development environment is set up as described in the [root README.md](../README.md). This includes
   `espup` and the necessary toolchains.
2. Connect your ESP32 board to your computer.
3. **Hardware Setup**: Connect an LED (with a current-limiting resistor) to the GPIO pin specified in the code (e.g.,
   GPIO8).
4. Navigate to this project's directory:
   ```bash
   cd blinky
   ```
5. Build, flash, and monitor the serial output using `cargo run`:
   ```bash
   cargo run --release
   ```
   This command will compile the application, flash it to your ESP32, and open a serial monitor. While the LED blinks,
   you might also see some initial boot messages on the serial monitor.

## Code Example

The core logic for this example is typically found in `src/bin/main.rs`:

```rust
#![no_std]
#![no_main]

use esp_backtrace as _;
use esp_hal::{
    clock::CpuClock,
    delay::Delay,
    gpio::{Io, Output, PushPull},
    main,
    peripherals::Peripherals,
};
use esp_println::println;
esp_bootloader_esp_idf::esp_app_desc!();

#[main]
fn main() -> ! {
    let peripherals = Peripherals::take();
    let io = Io::new(peripherals.GPIO, peripherals.IO_MUX);
    let mut led = io.pins.gpio8.into_push_pull_output(); // Example: Using GPIO8

    let delay = Delay::new();

    loop {
        led.toggle().unwrap();
        println!("LED Toggled");
        delay.delay_millis(500);
    }
}
```

**Note:** The specific GPIO pin (e.g., `gpio8`) might need to be adjusted based on your ESP32 board and wiring.