STM32 Advanced Timer Scheduling
Interrupt-Driven Output Compare with Dynamic Pulse Control

This project demonstrates advanced timer control on an STM32 microcontroller using TIM2 Output Compare (Toggle Mode) with interrupt-based scheduling.

Rather than using PWM, this implementation manually schedules compare events to generate a dynamically changing waveform. The design emphasizes precision timing, overflow safety, and non-blocking real-time control — techniques used in professional embedded systems.

🧠 Project Objective

To implement a deterministic, hardware-timed pulse generator using:

32-bit timer (TIM2)

Output Compare Toggle mode

Interrupt-based event scheduling

Modular arithmetic for overflow safety

The goal was to move beyond simple delay-based blinking and implement real embedded timing control.

⚙️ Technical Overview
Timer Configuration

Microcontroller: STM32 (TIM2 – 32-bit)

Clock Source: PLL @ 80 MHz

Prescaler: 79

Timer Frequency: 1 MHz

Resolution: 1 µs per tick

Auto-Reload (ARR): 0xFFFFFFFF

This makes the timer effectively free-running (~71-minute overflow).

Output Compare Mode

Channel configured in TOGGLE mode

Pin state changes automatically when:

CNT == CCR1

No software GPIO toggling required

🔄 Dynamic Interval Scheduling

Instead of fixed-period PWM, the next compare match is scheduled inside the interrupt:

next_compare += pulse_intervals[pulse_index];

This creates a progressively accelerating waveform using predefined intervals:

uint32_t pulse_intervals[] = {
    500000, 400000, 300000, 200000,
    100000, 50000, 25000, 12500
};

Because the timer runs at 1 MHz:

500000 → 500 ms

12500 → 12.5 ms

The sequence repeats continuously.

🔒 Overflow-Safe Design

The implementation is safe across timer overflows because:

TIM2 is 32-bit

next_compare is uint32_t

Unsigned arithmetic wraps modulo 2³²

Scheduling is incremental (not counter-referenced)

This mirrors techniques used in RTOS schedulers and real-time event systems.

🎯 Engineering Concepts Demonstrated

Hardware-timed deterministic control

Interrupt-driven scheduling

Modular arithmetic timing

Jitter avoidance via accumulated compare updates

Separation of hardware timing and application logic

This project reflects an understanding of how real embedded firmware avoids blocking delays and maintains precise timing.

📈 Practical Applications

The same architecture can be extended to:

Stepper motor acceleration profiles

Software frequency sweeps

Event-driven real-time systems

Communication timing protocols

Custom waveform generation

🛠️ Tools & Environment

STM32CubeIDE

STM32 HAL Drivers

C (Embedded)

Logic analyzer / oscilloscope validation

📌 Key Takeaway

This project demonstrates professional-level timer usage:

Deterministic, interrupt-driven hardware scheduling without blocking delays.

It represents a transition from beginner embedded programming to real-time system design thinking.
