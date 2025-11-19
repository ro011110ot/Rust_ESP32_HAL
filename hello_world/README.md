# Hello, World!

This is a classic "Hello, world!" example for the ESP32, demonstrating basic serial output using the `esp-hal` crate.

## Functionality

The application initializes the ESP32's peripherals and then enters an infinite loop. Within this loop, it prints "Hello World" to the serial console every 500 milliseconds, showcasing basic timing and serial communication.

## How to Run

1.  Ensure your development environment is set up as described in the [root README.md](../README.md). This includes `espup` and the necessary toolchains.
2.  Connect your ESP32 board to your computer.
3.  Navigate to this project's directory:
    ```bash
    cd hello_world
    ```
4.  Build, flash, and monitor the serial output using `cargo run`:
    ```bash
    cargo run --release
    ```
    This command will compile the application, flash it to your ESP32, and open a serial monitor to display the "Hello World" messages.

## Code Example

The core logic for this example is found in `src/bin/main.rs`:

```rust
#![no_std]
#![no_main]

use esp_backtrace as _;
use esp_hal::{
    clock::CpuClock,
    delay::Delay,
    main
};
use esp_println::println;
esp_bootloader_esp_idf::esp_app_desc!();


#[main]
fn main() -> ! {
    let config = esp_hal::Config::default().with_cpu_clock(CpuClock::max());
    let _peripherals = esp_hal::init(config);
    let delay = Delay::new();
    loop {
        println!("Hello World");
        delay.delay_millis(500);
    }
}
```