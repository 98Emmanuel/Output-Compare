STM32 TIM2 Output Compare – Dynamic Pulse Scheduler
📌 Overview

This project demonstrates advanced timer usage on an STM32 microcontroller using TIM2 Output Compare (Toggle Mode) with interrupt-driven scheduling.

Instead of using PWM or blocking delays, this implementation manually schedules each compare event inside the interrupt callback. The result is a deterministic, hardware-timed pulse generator with dynamically changing intervals.

This project highlights practical real-time embedded design techniques used in professional firmware development.

🎯 Project Objectives

Configure a 32-bit hardware timer (TIM2)

Implement Output Compare in TOGGLE mode

Use interrupt-based scheduling

Ensure overflow-safe timing using modular arithmetic

Avoid blocking functions such as HAL_Delay()

⚙️ Technical Configuration
Parameter	Value
MCU Timer	TIM2 (32-bit)
System Clock	80 MHz (PLL from HSI)
Prescaler	79
Timer Frequency	1 MHz
Timer Resolution	1 µs
ARR (Period)	0xFFFFFFFF

The timer runs as a free-running counter and overflows approximately every 71 minutes.

🔄 Dynamic Interval Logic

Pulse intervals are defined in microseconds:

uint32_t pulse_intervals[] = {
    500000, 400000, 300000, 200000,
    100000, 50000, 25000, 12500
};

The next compare match is scheduled incrementally:

next_compare += pulse_intervals[pulse_index];

This creates an accelerating toggle waveform while maintaining precise timing.

🔒 Overflow-Safe Design

Timing integrity is preserved because:

TIM2 is 32-bit

next_compare uses uint32_t

Unsigned arithmetic wraps modulo 2³²

Scheduling is incremental rather than counter-based

This technique is commonly used in RTOS schedulers and real-time embedded systems.

🧠 Concepts Demonstrated

Hardware-timed event scheduling

Interrupt-driven firmware architecture

Jitter-free timing accumulation

Modular arithmetic in embedded systems

Deterministic real-time control

🚀 Possible Extensions

Stepper motor acceleration profile

Frequency sweep generator

Software DDS implementation

Multi-channel scheduling system

RTOS-based task integration

🛠 Tools Used

STM32CubeIDE

STM32 HAL Drivers

C (Embedded Systems Programming)

Oscilloscope / Logic Analyzer for validation

👤 Author

Emmanuel Odongo
Embedded Systems Enthusiast
Focus: Real-Time Firmware & Low-Level MCU Development
