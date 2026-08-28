# ⏰ STM32 Digital Clock — RTC + OLED + CR2032

> **A tiny digital clock built around the STM32F103C8T6 Blue Pill, using the internal RTC and a CR2032 battery for timekeeping backup.**

![STM32 Digital Clock](images/clock.jpg)

---

## 🦊 Project Overview

What happens when you combine an **STM32 Blue Pill**, an **OLED display**, and a **CR2032 coin cell**?

A simple, compact digital clock!

This project demonstrates how to use the **Real-Time Clock (RTC)** peripheral of the **STM32F103C8T6** and display the current time on a **0.96-inch OLED**.

The CR2032 battery is connected to the STM32's **VBAT** pin, allowing the RTC to continue running when the main power supply is disconnected.

The entire project was built and tested on a breadboard using **STM32CubeMX** and **STM32CubeIDE**.

---

## ✨ Features

* ⏱️ STM32 internal RTC
* 🖥️ 0.96" OLED display
* 🔋 CR2032 RTC backup battery
* ⚡ STM32F103C8T6 Blue Pill
* 🕐 Real-time hour, minute and second display
* 🔌 RTC backup through the **VBAT** pin
* 🛠️ Configured with STM32CubeMX
* 💻 Developed using STM32CubeIDE
* 📐 Breadboard implementation

---

## 🧩 Hardware

| Component         | Description          |
| ----------------- | -------------------- |
| **STM32F103C8T6** | Main microcontroller |
| **0.96" OLED**    | Time display         |
| **CR2032**        | RTC backup battery   |
| **CR2032 Holder** | Battery connection   |
| **Breadboard**    | Prototype platform   |
| **Jumper Wires**  | Connections          |

---

## 🔌 Hardware Connections

### OLED

The OLED communicates with the STM32 using **I²C**.

| OLED | STM32F103C8T6 |
| ---- | ------------- |
| VCC  | 3.3V          |
| GND  | GND           |
| SCL  | I²C SCL       |
| SDA  | I²C SDA       |

### CR2032 → VBAT

The CR2032 battery is connected to the **VBAT** pin of the STM32.

```text
          CR2032
        +         -
        │         │
        │         └──────── GND
        │
        └────────────────── VBAT
                              │
                         STM32F103C8T6
                              │
                         Internal RTC
```

> ⚠️ **Important:** VBAT is intended for the RTC and backup registers. It is not a replacement for the STM32's main VDD supply.

---

## 🧠 How It Works

The STM32's internal **RTC peripheral** keeps track of:

```text
Hours
  ↓
Minutes
  ↓
Seconds
```

The current RTC values are periodically read by the firmware and sent to the OLED.

When the main STM32 supply is present:

```text
Main Power
    │
    ▼
 STM32
    │
    ├──► RTC
    │
    └──► OLED
```

When the main power is removed, the **CR2032 connected to VBAT** can keep the RTC domain powered:

```text
CR2032
   │
   ▼
 VBAT
   │
   ▼
 RTC
   │
   └──► Time is maintained
```

When the main power returns, the STM32 can read the RTC again and continue displaying the correct time.

---

## ⚙️ Software

The project was developed using:

* **STM32CubeMX** — peripheral configuration
* **STM32CubeIDE** — firmware development
* **HAL drivers**
* **RTC peripheral**
* **I²C peripheral**
* **OLED driver**

### Main Firmware Flow

```text
Initialize HAL
      ↓
Initialize GPIO
      ↓
Initialize I²C
      ↓
Initialize RTC
      ↓
Initialize OLED
      ↓
Read RTC time
      ↓
Format time
      ↓
Display on OLED
      ↓
Repeat
```

---

## 🕐 Display

The OLED displays the current time in a simple digital-clock format:

```text
┌──────────────────┐
│                  │
│     12:34:56     │
│                  │
└──────────────────┘
```

The display can be customized to show additional information such as:

* Date
* Day of the week
* Temperature
* Battery status
* Custom graphics

---

## 📁 Project Structure

```text
STM32-Digital-Clock/
│
├── Core/
│   ├── Inc/
│   └── Src/
│
├── Drivers/
│   └── OLED/
│
├── STM32CubeMX/
│   └── *.ioc
│
├── images/
│   └── clock.jpg
│
├── README.md
└── ...
```

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/STM32-Digital-Clock.git
```

### 2. Open the project

Open the project using **STM32CubeIDE**.

### 3. Check the CubeMX configuration

Open the `.ioc` file and verify the RTC and I²C configuration.

### 4. Connect the hardware

Build the circuit according to the wiring described above.

### 5. Build & Flash

Compile the project and program the STM32F103C8T6.

### 6. Enjoy your clock! ⏰

---

## 🎥 Project Video

This project is also demonstrated on **Sly Fox Electronics**, including:

* Hardware wiring
* STM32CubeMX configuration
* RTC configuration
* CubeIDE firmware
* OLED display
* CR2032 / VBAT backup operation

📺 **YouTube:** *[Add your video link here]*

---

## 🔮 Possible Improvements

This project can easily be extended into a more complete embedded clock:

* 📅 Date and calendar
* ⏰ Alarm functionality
* 🌡️ Temperature monitoring
* 🔘 Push-button time adjustment
* 🔋 Battery monitoring
* 🌙 Low-power mode
* 🎨 Custom OLED UI
* 📦 Custom PCB instead of breadboard
* 🕐 12/24-hour format selection

---

## 🦊 About

**Sly Fox Electronics** is a personal electronics and embedded-systems project channel focused on building real hardware and exploring:

**STM32 • Embedded Systems • PCB Design • FPGA • Analog Electronics**

---

### ⭐ If you found this project useful

Consider giving the repository a **star ⭐** and checking out the other projects from **Sly Fox Electronics**.

**Build it. Break it. Understand it. 🦊**
