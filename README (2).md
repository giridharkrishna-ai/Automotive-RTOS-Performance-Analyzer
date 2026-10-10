# Automotive RTOS Performance Analyzer

A real-time performance monitoring project for an automotive-style
embedded system. The application runs in a QNX-based environment and
records timing and GPIO-related behavior across repeated trials.

## Project Overview

The **Automotive RTOS Performance Analyzer** evaluates timing behavior
while coordinating hardware outputs. During each trial, the program
records:

-   **Distance (cm):** distance measurement reported by the sensor.
-   **Servo (degrees):** commanded servo position.
-   **LED:** LED output state (`ON` or `OFF`).
-   **Latency (ms):** measured response latency.
-   **Jitter (ms):** variation in timing between executions.
-   **Execution (ms):** reported execution duration for the trial.

The supplied console output shows **50 completed trials**, followed by
GPIO cleanup.

## Hardware and Software

Based on the project workspace and console output:

-   **Operating system / RTOS:** QNX
-   **Target platform:** Raspberry Pi 4 (the workspace is named
    `performance_rpi4`)
-   **Programming language:** C
-   **Hardware interface:** GPIO through the QNX GPIO resource manager
-   **Outputs:** servo control and LED state
-   **Sensor data:** distance measurements

Update this section if your final setup uses different hardware or
additional components.

## How It Works

1.  Initialize the required GPIO resources and communication.
2.  Run the trial sequence.
3.  Read or receive the distance value.
4.  Set the servo position and LED state according to the application
    logic.
5.  Record latency, jitter, and execution-time measurements.
6.  Repeat for 50 trials.
7.  Release GPIO resources during cleanup.

## Sample Performance Results

The values below are read from the supplied console screenshot. They
describe the displayed run and are not guaranteed performance limits.

  -----------------------------------------------------------------------
  Metric                                           Observed in screenshot
  ------------------------------ ----------------------------------------
  Number of trials                                                     50

  Reported latency                        Approximately 0.0066--0.0071 ms

  Reported execution time               Approximately 502.987--519.038 ms

  Jitter                         Usually small in many rows, with visible
                                                  spikes around 15--16 ms

  Run completion                                  All 50 trials completed

  Cleanup                                          GPIO cleanup completed
  -----------------------------------------------------------------------

### Important Observation

The latency values are consistently around 0.0066--0.0071 ms in the
displayed output, but several jitter readings are much higher (around
15--16 ms), and execution time varies between roughly 503 ms and 519 ms.
Investigate these outliers before claiming fully deterministic timing.
Confirm the units, timing source, and whether the jitter calculation
includes scheduling delays or measurement artifacts.

## Building and Running

Build and run the project using the configured QNX Momentics IDE
workspace and the project's existing `Makefile`.

1.  Open the project in QNX Momentics IDE.
2.  Confirm the correct target/build configuration is selected.
3.  Build the project.
4.  Connect to the target device and verify GPIO access and hardware
    wiring.
5.  Run the application and save the console output for analysis.

Exact command-line build and launch commands depend on your QNX SDK,
target configuration, and Makefile settings.

## Repository Structure

The workspace screenshot shows a layout similar to:

``` text
performance_rpi4/
├── src/
│   ├── performance_rpi4.c
│   ├── rpi_gpio.c
│   └── rpi_gpio.h
├── includes/
├── build/
└── Makefile
```

Your actual repository may differ; adjust this tree to match the files
you commit.

## Future Improvements

-   Export trial data to CSV for repeatable analysis.
-   Calculate minimum, maximum, average, and percentile latency and
    jitter.
-   Add plots for latency, jitter, and execution time across all trials.
-   Repeat tests under CPU load and document the test conditions.
-   Investigate the large jitter spikes and validate timing units.
-   Document the exact sensor, servo, GPIO pin mapping, and wiring.

## Notes

This README is based on the screenshots provided. Replace inferred
hardware details with the exact setup used in your final implementation,
and include only performance claims supported by repeatable
measurements.
