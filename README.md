# STM32F103C8T6 LED Blinking with FreeRTOS and Preemptive Scheduling
This project demonstrates how to use FreeRTOS with a priority-based preemptive scheduling policy on an STM32F103C8T6 microcontroller. Two tasks are created to control the blinking of red and green LEDs, each assigned different priorities to illustrate task preemption in real-time systems.

## Features
- RTOS: FreeRTOS with priority-based preemptive scheduling.
- LED Blinking: Two tasks control the red and green LEDs on the STM32F103C8T6.
  1. Red LED Task: Higher priority, blinks 10 times quickly.
  2. Green LED Task: Lower priority, blinks 80 times, preempted by the red LED task.
- Task Control: Demonstrates task scheduling, preemption, and delays using FreeRTOS.

## Hardware Requirements
1. Microcontroller: STM32F103C8T6.
2. Breadboard.
3. LEDs: External LEDs (Red and Green), or you can use onboard LEDs if available.
4. IDE/Toolchain: STM32CubeMX, STM32CubeIDE, or any supported ARM GCC toolchain.

## Software Requirements
1. HAL Library: STM32 HAL library for GPIO and system configuration.
2. FreeRTOS: Real-Time Operating System for task scheduling.

## Circuit Description

- **Pin PA11** is connected to the positive leg of the **Green LED**, which is responsible for running a task.
- **Pin PA10** is connected to the positive leg of the **Clear LED**, which acts as an indicator that the task is running.
- **Pin PA9** is connected to the positive leg of the **Red LED**, which is responsible for running another task.
- **Pin PA8** is connected to the positive leg of another **Clear LED**, which also acts as an indicator that the task is running.
- All negative legs of the LEDs are connected to **pull-down resistors**.
- The remaining legs of the resistors are connected to **ground**.

This setup ensures that the tasks are indicated clearly by the respective LEDs, and pull-down resistors help stabilize the LED states.

## How It Works
### 1. Red LED Task (Higher Priority):
The red LED task has a higher priority (osPriorityAboveNormal).
It blinks the red LED 10 times, with a delay of 25ms between toggles.   
The task preempts the green LED task when both are ready to run.
After 10 blinks, it goes into a 1.5 second delay (osDelay(1500)).

### 2. Green LED Task (Lower Priority):
The green LED task has a normal priority (osPriorityNormal).
It blinks the green LED 80 times, with a 25ms delay between each toggle.
If the red LED task becomes ready to run, the green LED task is preempted.
After completing 80 blinks, it goes into a 6-second delay (osDelay(6000)).

### 3. Scheduler:
FreeRTOS kernel starts after initialization and manages task scheduling based on priority.
The red LED task preempts the green LED task when both are active.

## Steps to Run the Program
### 1. Setup STM32CubeMX:
Select the STM32F103C8T6 microcontroller.
Enable GPIO for the LED pins.
Enable FreeRTOS in the middleware settings.
### 2. Configure Tasks:
In STM32CubeMX, configure two tasks (RED_LED_TASK and GREEN_LED_TASK) with different priorities.
### 3. Generate Code:
Generate the project code from STM32CubeMX for your IDE (STM32CubeIDE, Keil, etc.).
### 4. Build and Flash:
Build the project and flash it to the STM32F103C8T6 using ST-Link or a similar programmer.
### 5. Observe Behavior:
The green LED will blink continuously, but when the red LED task becomes ready (every 1.5 seconds), it will preempt the green LED task and blink the red LED.

## Circuit Form
![rangkaian task indicator](https://github.com/user-attachments/assets/86252673-0c9e-47e0-88e0-c02d4e0bcd8c)

## Demo Video
[task_indicatorr2](https://github.com/user-attachments/assets/9ea35fd7-b34a-47f3-b811-3f1afa42708d)






