
# Morse Code Learning Game

**An interactive, four-level Morse Code learning game developed for the Raspberry Pi Pico using C and ARM assembly.**

A collaborative embedded-systems project completed as part of **CSU23021 – Microprocessor Systems** at **Trinity College Dublin** in 2023.

![Assignment 02 – Morse Code Game](https://user-images.githubusercontent.com/91458920/225872537-d8e3db8b-ddfd-4d5d-a648-d2d98993b9c4.png)

## Overview

The Morse Code Learning Game is an educational embedded application that teaches players to recognise and enter Morse Code through a physical push-button interface.

Developed for the **MAKER-PI-PICO board**, the game combines C for application logic with ARM assembly for low-level input processing and interrupt handling. Players enter Morse Code using the board's GP21 button, receive feedback through a serial console and RGB LED, and progress through increasingly challenging levels.

The project was developed by a five-person team over four weeks, with an emphasis on embedded programming, hardware interaction, collaborative software development, version control and systematic testing.

## Features

- **Four difficulty levels**, progressing from individual characters to complete words.
- **Physical Morse Code input**, using short and long button presses to distinguish dots and dashes.
- **Alphanumeric decoding**, supporting letters A–Z and digits 0–9.
- **Interactive UART console**, displaying instructions, questions, decoded input and game feedback.
- **Lives system**, with incorrect answers reducing lives and correct answers restoring lives up to a maximum of three.
- **Level progression**, requiring five consecutive correct sequences to advance.
- **RGB LED feedback**, communicating the current game state.
- **Watchdog timer**, supporting automatic recovery following inactivity.
- **Performance statistics**, tracking correct answers, incorrect answers and success rates.

## Gameplay

The game supports four progressively challenging levels.

| Level | Difficulty | Challenge | Morse Reference |
|---|---|---|---|
| **1** | Easy | Translate individual characters | Provided |
| **2** | Medium | Translate individual characters | Hidden |
| **3** | Hard | Translate complete words | Provided |
| **4** | Expert | Translate complete words | Hidden |

### Entering Morse Code

The player interacts with the game through the **GP21 push-button** on the MAKER-PI-PICO board.

- A short press represents a dot (`.`).
- A longer press represents a dash (`-`).
- Pauses between button presses are used to distinguish Morse Code symbols and completed input sequences.
- The decoded input is displayed through the serial console.

### Progression and Feedback

Players begin with three lives. Incorrect sequences reduce the remaining lives, while correct sequences can restore a life up to the maximum.

Completing five consecutive correct sequences allows progression to the next level.

The RGB LED provides visual feedback, while console messages display the player's progress, answer accuracy and game status.

## Technical Implementation

The application integrates higher-level game logic with low-level embedded hardware control.

### C – Game Logic and Hardware Integration

The C implementation manages the core gameplay and interfaces with the Raspberry Pi Pico SDK.

Responsibilities include:

- Initialising the Morse Code lookup table.
- Representing alphanumeric characters and their Morse Code sequences.
- Validating player input against expected answers.
- Tracking difficulty levels, lives and correct responses.
- Displaying game instructions and feedback.
- Calculating performance statistics.
- Controlling the WS2812 RGB LED through the PIO interface.
- Configuring the watchdog timer.
- Providing C wrappers for GPIO operations used by the assembly implementation.

**Source:** [`assign02.c`](assign02.c)

### ARM Assembly – Input Processing and Interrupt Handling

The ARM assembly component implements low-level control of the physical input interface.

The program uses the RP2040's Cortex-M0+ instruction set to coordinate button input and game execution.

Key responsibilities include:

- Configuring GPIO input.
- Installing interrupt service routines.
- Detecting button presses and releases.
- Processing timing information to distinguish Morse Code symbols.
- Managing input sequences.
- Coordinating execution between assembly routines and C functions.

**Source:** [`assign02.S`](assign02.S)

### Programmable I/O and RGB LED

The project uses the RP2040 Programmable I/O (PIO) subsystem to control the board's WS2812 RGB LED.

The LED provides a visual representation of game state and player feedback.

**Source:** [`ws2812.pio`](ws2812.pio)

## Hardware and Technology

| Component | Technology |
|---|---|
| Microcontroller | Raspberry Pi RP2040 |
| Development board | MAKER-PI-PICO |
| Programming languages | C and ARM Thumb assembly |
| SDK | Raspberry Pi Pico SDK |
| Build system | CMake |
| Compiler toolchain | ARM GNU Toolchain |
| User input | GP21 push-button |
| Visual feedback | WS2812 RGB LED |
| Console | UART serial communication |
| Hardware interfaces | GPIO interrupts, PIO and watchdog timer |
| Version control | Git and GitHub |

## Repository Structure

```text
.
├── CMakeLists.txt       # Build configuration
├── assign02.c           # Game logic and hardware integration
├── assign02.S           # ARM assembly input and interrupt handling
├── ws2812.pio           # RGB LED PIO program
├── ws2812.pio.h         # Retained PIO header
├── build/               # Archived build outputs and firmware
└── README.md            # Project documentation
```

The repository preserves the original collaborative Git history and its archived build artifacts.

## Building and Running

The project targets the Raspberry Pi Pico and requires an appropriate embedded development environment.

### Requirements

- Raspberry Pi Pico or compatible RP2040 board
- Raspberry Pi Pico SDK
- ARM GNU Toolchain
- CMake
- Compatible build tools
- USB connection and serial terminal
- MAKER-PI-PICO board for the intended physical input and LED interface

### Build Configuration

The [`CMakeLists.txt`](CMakeLists.txt) configuration defines the application's C and assembly source files, links the relevant Pico libraries and generates firmware outputs.

The original project was developed within a Pico applications environment. Its CMake configuration uses `apps_auto_set_url()`, so building it independently may require restoring the original parent-project configuration or adapting that setting.

### Firmware

The archived [`build/`](build/) directory includes historical build outputs, including an `.elf` executable and `.uf2` firmware image.

The `.uf2` file is intended for deployment to the Raspberry Pi Pico using its USB bootloader.

## Development Process

The project was developed between **March and April 2023** using a collaborative GitHub workflow.

The team organised development into three major implementation versions:

1. **Version 1.0:** Initial implementation of the core game requirements and integration testing.
2. **Version 2.0:** Refinement of the standard two-level game, code review and further testing.
3. **Version 3.0:** Expansion to four levels, additional statistics, documentation and final testing.

The team used:

- GitHub Issues to track requirements and tasks.
- Feature branches for individual development work.
- Pull requests for integrating contributions.
- A dedicated testing branch for integration and validation.
- Git commit history to track collaborative development.

The original project history has been preserved in this repository, retaining the contributions and development work of the full team.

## Team and Contributions

This project was completed collaboratively by **Group 14**.

| Contributor | Project Responsibility |
|---|---|
| **Leah Weldon** | Project Code Owner |
| **Faith Olopade** | Project Workflow Owner |
| **Ingrid Rønneberg Bustnes** | GitLab Workflow Owner and GitHub repository management |
| **Martha Ryan** | Project Documentation Owner |
| **Della Doherty** | Project Demonstration Owner |

All five members contributed to the development of the application.

### My Contributions

As **Project Code Owner**, my responsibilities included code implementation, testing and integration quality across the project's development stages.

My documented contributions included:

- Implementing and refining the functionality associated with Requirement 5 across Versions 1.0, 2.0 and 3.0.
- Contributing to Morse Code input validation and comparison with expected sequences.
- Implementing RGB LED-related functionality.
- Contributing to ARM assembly input handling and interrupt processing.
- Testing integrated implementations during each major development iteration.
- Performing code cleanup and contributing code documentation.

The original source files also retain function-level author annotations identifying contributions from individual team members.

### Original Collaborative Repository

The original team repository was maintained under Ingrid Bustnes's GitHub account:

[IngridBustnes/CSU23021-GRP14](https://github.com/IngridBustnes/CSU23021-GRP14)

This repository preserves the original Git history in a standalone project archive.

## Project Documentation

The team prepared supporting documentation and an application demonstration as part of the original assessment.

The original project documentation covered the implementation, development workflow, testing process and individual team responsibilities.

The complete collaborative source code and commit history are preserved in the [original Group 14 repository](https://github.com/IngridBustnes/CSU23021-GRP14).

Additional project documentation and demonstration materials were maintained separately as part of the university submission.

## Academic Context

**University:** Trinity College Dublin  
**Course:** Computer Science  
**Module:** CSU23021 – Microprocessor Systems  
**Academic Year:** 2022–2023  
**Assignment:** Group Assignment 02  
**Group:** 14  
**Development Period:** 20 March – 9 April 2023

## Archive Note

This repository preserves the original collaborative source code, build artifacts and Git commit history for the Group 14 Morse Code Learning Game.

The project was designed for specific embedded hardware and an academic Pico SDK development environment. Reproducing its original behaviour may require compatible hardware and build dependencies.

The repository is maintained as a portfolio archive of a collaborative university project, with team responsibilities and individual contributions attributed accordingly.

---

> Developed collaboratively by Group 14 as part of **CSU23021 – Microprocessor Systems**, Trinity College Dublin, 2023.
