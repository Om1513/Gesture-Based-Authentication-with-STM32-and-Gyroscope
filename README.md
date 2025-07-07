# Gesture-Based Authentication with STM32 and Gyroscope

This project implements a gesture-based passkey authentication system using the STM32F429ZI development board, an onboard gyroscope (L3GD20), and an LCD screen. The user sets a "gesture passkey" using wrist movements, which is later matched using Dynamic Time Warping (DTW) to authenticate or unlock the system.

## 🚀 Features

- SPI Communication with L3GD20 gyroscope
- Real-time angular velocity processing
- Dynamic Time Warping (DTW) to compare gesture similarity
- LCD display feedback and graphics on the STM32F429ZI
- Interrupt-driven user input
- Finite State Machine (FSM) managing UI states and user interaction

## 📦 Project Structure

```
Project/
├── include/              # Header files (currently unused)
├── lib/                  # External libraries (if any)
├── src/
│   ├── main.cpp          # Main application with FSM, SPI, DTW, LCD
│   └── SPI.comments      # Annotated reference code (SPI, polling, interrupts)
├── test/                 # Testing code (if extended)
├── .mbedignore
├── .gitignore
├── mbed_app.json         # Mbed config file
├── platformio.ini        # PlatformIO project settings
└── README.md             # This file
```

## 🧠 How It Works

1. IDLE: Displays prompt to record gesture.
2. RECORD: Captures angular velocity from gyroscope over time.
3. ENTER: Captures another gesture attempt.
4. PROCESS: Uses DTW to compare the attempt to the stored passkey.
5. UNLOCK or FAIL: Displays result on LCD.

The gesture is captured as a time series of angular velocity across X, Y, Z axes. The comparison is done using DTW, which accounts for temporal variation in movement.

## 🔧 Setup & Usage

### Requirements

- STM32F429ZI Discovery Board
- Mbed OS
- PlatformIO (or Mbed CLI)
- Serial terminal (e.g., Tera Term, PuTTY) for debug logs
- LCD screen (included on STM32F429ZI board)

### Build & Flash

With PlatformIO:

```bash
platformio run --target upload
```

Or using Mbed CLI:

```bash
mbed compile -m DISCO_F429ZI -t GCC_ARM
mbed flash
```

### Serial Monitor

To view logs:

```bash
platformio device monitor
```

## 📷 LCD UI

- Displays instructions and success/failure messages
- Shows a smiley face upon successful unlock
- Uses character-by-character rendering for prompts

## ✍️ Files of Interest

- main.cpp: Core implementation with FSM, gesture capture, filtering, DTW, and LCD UI
- SPI.comments: Reference code snippets on SPI config, interrupts, and polling for gyroscope

## 📚 Concepts Used

- SPI Communication (blocking + async)
- Interrupt Handling
- Button Debouncing
- Digital Filtering (Exponential Moving Average)
- DTW (Dynamic Time Warping) for time-series comparison
- LCD graphics using STMicroelectronics LCD API

## 🤝 Contributions

Want to build gesture-based passwords into your own projects or help optimize the DTW performance? PRs and forks welcome.

## 🛠️ Future Improvements

- Save passkeys to flash for persistence
- Add support for more gestures
- Integrate voice or additional sensors
