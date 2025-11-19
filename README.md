# Rust ESP32-HAL Workspace

This workspace contains a collection of examples for the ESP32 using the `esp-hal` crate.

## Projects

*   `blinky`: A simple example that blinks an LED.
*   `button_pressed`: An example that demonstrates reading a button press.
*   `hello_world`: A classic "Hello, world!" example that prints to the console.

## Setup and Installation

These instructions are based on the guide [Embedded Rust on the ESP32: Getting started - Setup](https://dev.to/vaishnav_sabari_girish/embedded-rust-on-the-esp32-getting-started-setup-28en).

### 1. Install `espup`

`espup` is a tool to install and maintain the Rust toolchains for ESP32 development.

```bash
cargo install espup
```

### 2. Install the Toolchain

This command will install the necessary toolchains, including the Xtensa Rust toolchain and the `esp-idf` build tools.

```bash
espup install
```

### 3. Set Environment Variables

After installation, `espup` will provide a command to set the required environment variables. You must add this command to your shell's startup file (e.g., `.profile`, `.bashrc`, or `.zshrc`).

The command will look something like this:

```bash
source $HOME/.cargo/env
```

**Important:** You need to restart your shell or source the startup file for the changes to take effect.

## Building and Flashing

To build and flash a specific project within this workspace, navigate to its directory and use `cargo-espflash`. The `espup install` command should have already installed it.

```bash
cd blinky
cargo espflash flash --monitor
```

This command will:
1.  Build the project.
2.  Flash the resulting binary to the connected ESP32.
3.  Open a serial monitor to view the output.