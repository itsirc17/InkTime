# InkTime

Designed for optimal energy efficiency, InkTime is a custom e-paper smartwatch project. This document serves as a complete technical reference for the project.

## Block Diagram(Architecture)

```mermaid
graph TD
    %% Central MCU
    MCU[nRF52840 Microcontroller]

    %% Power Subsystem
    USB[USB-C Port] -->|5V VBUS| ESD[ESD Protection USBLC6]
    ESD -->|5V| CHG[BQ25180 LiPo Charger]
    DCDC -->|3.3V System Power| MCU
    DCDC -->|3.3V| SENSORS
    BATT[LiPo Battery] <--> CHG
    BATT <--> FG[MAX17048 Fuel Gauge]
    BATT -->|V_BAT| DCDC[RT6160 Buck-Boost DC/DC]

    %% Interconnects
    MCU <-->|I2C Bus| IMU[BMA421 Accelerometer]
    MCU <-->|I2C Bus| HAP[DRV2605 Haptic Driver]
    MCU <-->|I2C Bus| CHG
    MCU <-->|I2C Bus| FG

    MCU -->|SPI & Control| EPD[E-Paper Display Connector]
    MCU -->|PWM/Trigger| HAP
    HAP -->|Analog| LRA[Haptic Motor]

    %% Inputs
    BTN1[SW_UP] -->|GPIO| MCU
    BTN2[SW_ENT] -->|GPIO| MCU
    BTN3[SW_DN] -->|GPIO| MCU

    %% SWD
    SWD[TC2030-IDC SWD Port] <-->|Programming/Debug| MCU
```
