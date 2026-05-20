# 🎮 AXIOM-CORE-INPUT

### Next-Gen Bare-Metal Firmware for Magnetic Levitation Controllers ⚡

`axiom-core-input` is a high-performance, ultra-low latency firmware written completely in native **Rust**. Designed for hardware architectures utilizing magnetic levitation analog joysticks and Hall-effect triggers, it completely bypasses traditional operating system input-stack overhead by processing raw hardware interrupts directly in the firmware layer.

By achieving a **native 8000 Hz polling rate**, this architecture guarantees a real input processing pipeline of **sub-1.1ms**, delivering telemetry data to host machines at the absolute speed of thought.

---

## 🚀 Key Specifications

| Feature | Specification | Technical Impact |
| :--- | :--- | :--- |
| **Language** | Rust (`no_std` core) | Zero garbage collection, memory safety, bare-metal speed |
| **Polling Rate** | 8000 Hz (Native USB/BLE) | Telemetry updates every 0.125ms directly to the host |
| **Hardware Latency**| Sub-1.1ms Real Target | Minimal delta between physical input and register shift |
| **Sensor Tech** | Analog Magnetic Levitation | Zero-friction, Hall-effect driftless coordinates |
| **Processing** | Direct Interrupt Registers | Bypasses general-purpose OS USB polling cycles |

---

## 🛠️ Architecture Overview
The system runs as an independent bare-metal firmware layer. Instead of waiting for the operating system to poll the device, `axiom-core-input` pushes high-density coordinate matrix packets directly onto the bus using dedicated high-speed DMA (Direct Memory Access) channels.

## 📁 Project Structure

```text
axiom-core-input/
├── Cargo.toml
├── src/
│   ├── main.rs              # Firmware entry point and hardware initialization
│   ├── interrupt.rs         # Direct DMA and High-Speed USB timer ISRs
│   ├── adc/
│   │   ├── mod.rs           # ADC configuration matrix
│   │   └── magnetic.rs      # Hall-effect levitation analog sampling core
│   ├── usb/
│   │   ├── mod.rs           # 8000Hz USB composite device descriptor
│   │   └── dma.rs           # Ultra-low latency Direct Memory Access channels
│   └── filter/
│       └── kalman.rs        # High-frequency jitter mitigation algorithms
└── tests/
    └── latency_tests.rs     # Bare-metal sub-1.1ms integration benchmarks

## ⚙️ Building and Deployment

This firmware is designed to target embedded ARM Cortex-M7 microcontrollers (`thumbv7em-none-eabihf`). It compiles entirely in `#![no_std]` mode.

### Prerequisites

1. Install the Rust bare-metal compilation target:
```bash
rustup target add thumbv7em-none-eabihf
```

2. Install the hardware flashing utility (probe-rs):
```bash
cargo install probe-rs --features cli
```

Compilation
To compile the firmware stack in release mode with maximum optimization passes (opt-level = 3):
```bash
cargo build --release --target thumbv7em-none-eabihf
```

Running Latency & Telemetry Benchmarks
To validate the sub-1.1ms processing pipeline matrix, execute the hardware simulation integration tests:
```bash
cargo test --test latency_tests --target thumbv7em-none-eabihf
```

The system runs as an independent bare-metal firmware layer. Instead of waiting for the operating system to poll the device, `axiom-core-input` pushes high-density coordinate matrix packets directly onto the bus using dedicated high-speed DMA (Direct Memory Access) channels.
