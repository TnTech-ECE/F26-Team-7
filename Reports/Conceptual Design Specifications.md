# Conceptual Design


## High-Level Solution

Team 7 plans to develop a PLC-based monitoring and control system for Flexial's cleaning and passivation processes. The system will use sensors, a PLC, and a user interface to monitor tank conditions, record data, and improve process efficiency. The system will also track parts using barcode scanning and communicate with Flexial's existing software.

#### Proposed Design:

The project will be divided into five main subsystems: cleaning sensors, passivation sensors, PLC hardware, barcode scanning, and Flexnet/Epicor communication. These subsystems will work together to collect, display, and store process information.

#### Cleaning Subsystem:

The cleaning subsystem will monitor tank conditions using temperature, pH, TDS, concentration, conductivity, water flow, and air flow measurements. It will also monitor oven temperatures.

The operator will start and stop the cleaning process through the interface. During operation, the PLC will collect sensor readings and display them for the operator. If a reading falls outside the acceptable range, the interface will display a warning.

#### Passivation Subsystem:

The passivation subsystem will monitor temperature, pH, TDS, concentration, water flow, and thickness measurements.

The operator will start and stop the passivation process through the interface. The PLC will also automatically control draining and reconcentration when needed. This will help maintain the required chemical conditions and reduce manual adjustments.

#### PLC and User Interface:

The PLC will collect information from the sensors and send it to the user interface. Operators will be able to view sensor readings, start and stop processes, and receive warnings when problems occur.

The system will use one main PLC and a shared interface for both cleaning and passivation.

#### Barcode Scanning:

The barcode system will allow operators to scan part numbers before starting a process. The PLC will associate the part number with the recorded sensor data.

Once the process is finished, the part number and process information will be saved for future reference.

#### Flexnet and Epicor Communication:

The system will be designed to communicate with Flexial's existing Flexnet and Epicor software. This will help transfer and organize part numbers, sensor readings, and process records.

#### Meeting Project Goals:

The main goal of this project is to improve how Flexial monitors and records its cleaning and passivation processes.

The system will reduce manual data recording, make sensor readings easier to access, and improve part tracking. Automatic draining and reconcentration during passivation will also help reduce the amount of manual work required from operators.

#### Requirements and Constraints:

Team 7 will design the system around Flexial's requirements, available equipment, and project timeline.

The current budget target is approximately **$49,500**, including contingency. This is a preliminary estimate, and equipment prices will be updated as components are selected.

The team will also make sure the selected sensors, PLC equipment, and communication systems are suitable for the required processes.

#### Risk Reduction:

The system will display warnings when sensor readings fall outside acceptable limits. This will help operators identify problems during cleaning and passivation.

The automatic passivation functions will include safety checks to help prevent incorrect draining or reconcentration. Team 7 will also test the sensors, PLC communication, barcode scanning, and data recording to make sure the system works correctly.

#### Resource Utilization:

The project will use one PLC and a shared user interface for both cleaning and passivation. This will reduce duplicate equipment and help control costs.

Separating the project into subsystems will make programming, testing, and troubleshooting easier. Flexial will also provide programming and software integration support, helping the team stay within the project budget.

### Hardware Block Diagram

Block diagrams are an excellent way to provide an overarching understanding of a system and the relationships among its individual components. Generally, block diagrams draw from visual modeling languages like the Universal Modeling Language (UML). Each block represents a subsystem, and each connection indicates a relationship between the connected blocks. Typically, the relationship in a system diagram denotes an input-output interaction.

In the block diagram, each subsystem should be depicted by a single block. For each block, there should be a brief explanation of its functional expectations and associated constraints. Similarly, each connection should have a concise description of the relationship it represents, including the nature of the connection (such as power, analog signal, serial communication, or wireless communication) and any relevant constraints.

The end result should present a comprehensive view of a well-defined system, delegating all atomic responsibilities necessary to accomplish the project scope to their respective subsystems.

<img width="1776" height="1186" alt="image" src="https://github.com/user-attachments/assets/cec01598-f38d-4a80-8667-938ba793018f" />


### Operational Flow Chart

# PLC System Flowcharts

## Cleaning Subsystem

<img width="1324" height="1334" alt="image" src="https://github.com/user-attachments/assets/b2076098-2e7e-467c-b52e-6f9411ee96f2" />

## Passivation Subsystem

<img width="1614" height="1320" alt="image" src="https://github.com/user-attachments/assets/65a4be8e-332f-4415-95be-516fc2c62808" />

## Atomic Subsystem Specifications

### Barcode Scanner and Validation Subsystem:

This subsystem obtains the data by using a barcode scanner to take in an input of a part starting or leaving the cleaning or passivation process. It will scan the barcode on the part itself and convert that code into a data string that will go through each step of its respective process as each step is completed. Once the part is done in either process, the part is checked for validation by measuring the thickness of the part before and after to find how much material was removed. If the correct amount was removed, the part is validated and moves to the next process.

Barcode Scanner:
- Signal: Digital
- Direction:  Input to PLC
- Protocols: Communicates with PLC
- Sends String Data to PLC

Validation:
- Signal: Digital
- Direction:  Input and Output to PLC
- Protocols: Validated through Epicor and flexnet 
- Data Sent: String of Thickness, then Boolean for Validation

Requirements:
- The subsystem shall take a barcode input and store that string until the part is scanned out.
- The subsystem shall measure the thickness of the part before and after the part comes into its respective process. If the part has too much material removed or not enough material removed, reject the part. If the part meets the required material reduction, the part is accepted and moves to the next process.

### Cleaning Sensors, Timers, and Lights Subsystem:

This subsystem will continuously read physical sensors for all four tanks in the cleaning process and convert the obtained 4-20 mA data into measurable quantities with proper units. The sensors used will be pH, Concentration, Conductivity, TDS, Temperature, Water flow, and Air flow. When a part enters each step of the cleaning process, a timer is started. When the part has been in its respective step for the required amount of time, the time latches as done and turns on a light for that step. The part is then put into the next step of cleaning. 

Sensors:
- Signal: 4-20mA analog 
- Direction:  Input to PLC
- Protocols: Current loop
- Data Sent: Loop currents with a value of 4-20mA, which are then converted to pH, TDS, Conductivity, Temperature, Water flow, or Air flow depending on the sensor.

Lights:
- Signal: 120 Vac
- Direction: Output for PLC
- Protocols: Controlled by PLC
- Data Sent: Binary Boolean for on and off

Requirments:
- The subsystem shall convert the 4-20mA currents obtained from the sensors to usable values.
- The subsystem shall ensure that when the specified amount of time has passed for a part to be in a tank, the light turns on.
- The subsystem shall alert the user when the conductivity of tank 4 exceeds 20 S.

### Passivation Sensors, Timers, and Lights:

This subsystem monitors the 3 Nitric acid tanks using pH, temperature, TDS, and concentration sensors; the Nitric acid and hydrofluoric acid pickling tank using pH, Temperature, TDS, and Concentration sensors; the two immersion rinse tanks using TDS, Temperature, Concentration, and pH sensors; and the one manual rinse tank using only a water flow sensor. It will read and convert the 4-20mA values from the sensors and send those values to the PLC. Timers will start when a part goes into a tank, and once the time for the part in that tank is completed, the light turns on to notify that the part is ready for the next step of passivation.

Sensors:
- Signal: 4-20mA analog 
- Direction:  Input to PLC
- Protocols: Current loop
- Data Sent: Loop currents with a value of 4-20mA, which are then converted to Temperature, pH, TDS, Concentration, and Water flow.

Lights:
- Signal: 120 Vac
- Direction: Output to PLC
- Protocols: Communicates with PLC
- Data Sent: Binary Boolean for on and off

Requirements:
- The subsystem shall convert the 4-20mA currents obtained from the sensors to usable values.
- The subsystem shall ensure that when the specified amount of time has passed for a part to be in a tank, the light turns on.

### PLC to Server Subsystem:

This subsystem will communicate the information stored in the PLC to the web server so that the information on where a part is in the fabrication process and in each of the subprocesses and steps a part is at can be viewed online via a web browser. It will sync with Flexial’s Epicor ERP/FlexNet servers.

Requirements:
- The subsystem shall establish a one-way data transfer from the PLC to the server.
- The subsystem shall update the values in the server within 1 second of the values being updated on the PLC.
- The subsystem shall allow a user to remotely view the data in the PLC to see where a part is in the fabrication process.
- The subsystem shall block outside data from coming in and affecting the PLC so that security and safety is ensured and no I/O logic or pins can be overwritten.

### User Interface
The system will run into Optix. This is a way of displaying the HMI style interface onto a server. 

- The subsystem shall give a user friendly way to monitor data points and see that they are recorded.

## Ethical, Professional, and Standards Considerations

In the project proposal, each team must evaluate the broader impacts of the project on culture, society, the environment, public health, public safety, and the economy. Additionally, teams must consider relevant standards organizations that will inform the design process. A comprehensive discussion should be included on how these considerations have influenced the design. This includes detailing constraints, specifications, and practices implemented as a result, and how these address the identified considerations.


## Resources


### Budget

# Team 7: Revised Budget Document

## Project Budget Overview

Team 7 has an estimated budget of **$40,000–$50,000** for the Flexial PLC Programming and Process Controls project. The budget has been divided into five subsystems: cleaning sensors, passivation sensors, PLC hardware and controls, barcode scanning, and Flexnet/Epicor communication.

The current estimated project cost is **$49,500**, including contingency. All PLC hardware, sensors, and valves will need to be purchased. Flexial will handle the programming and software integration, helping reduce overall project costs.

## 1. Cleaning Sensors

This subsystem includes the sensors needed to monitor the cleaning tanks and oven conditions.

| Equipment | Quantity | Unit Price ($) | Total ($) |
|---|---:|---:|---:|
| pH Sensors | 3 | 500 | 1,500 |
| TDS Sensors | 3 | 450 | 1,350 |
| Temperature Sensors | 5 | 150 | 750 |
| Concentration Sensor | 1 | 1,500 | 1,500 |
| Conductivity Sensor | 1 | 500 | 500 |
| Water Flow Sensor | 1 | 400 | 400 |
| Air Flow Measurements | 2 | 500 | 1,000 |
| **Cleaning Subtotal** | | | **7,000** |

## 2. Passivation Sensors

This subsystem includes the sensors used to monitor the passivation tanks and chemical conditions.

| Equipment | Quantity | Unit Price ($) | Total ($) |
|---|---:|---:|---:|
| pH Sensors | 6 | 500 | 3,000 |
| TDS Sensors | 6 | 450 | 2,700 |
| Temperature Sensors | 6 | 150 | 900 |
| Concentration Sensors | 6 | 1,500 | 9,000 |
| Water Flow Sensor | 1 | 400 | 400 |
| Thickness Measurements | 2 | 500 | 1,000 |
| **Passivation Subtotal** | | | **17,000** |

## 3. PLC Hardware and Controls

This subsystem includes the main PLC equipment, input/output modules, user interface, and valves needed to monitor and control the processes.

| Equipment | Quantity | Total ($) |
|---|---:|---:|
| PLC Processor | 1 | 2,500 |
| PLC Memory / Storage | 1 | 200 |
| Power Supply | 1 | 400 |
| Analog Input Modules | TBD | 4,000 |
| Digital I/O Modules | TBD | 1,500 |
| User Interface | 1 | 1,500 |
| Fill Valves | 6 | 1,800 |
| Drain Valves | 6 | 1,800 |
| Control Cabinet and Wiring | 1 | 2,000 |
| Safety Equipment / Relays | TBD | 1,300 |
| PLC Network Equipment | TBD | 1,000 |
| **PLC Subtotal** | | **18,000** |

## 4. Barcode Scanning

This subsystem will allow operators to scan part numbers and associate them with recorded process information.

| Equipment | Quantity | Total ($) |
|---|---:|---:|
| Barcode Scanner | 1 | 650 |
| Scanner Communication Hardware | 1 | 200 |
| Part Number Storage Setup | 1 | 150 |
| **Barcode Subtotal** | | **1,000** |

## 5. Flexnet / Epicor Communication

This subsystem will allow the PLC system to communicate with Flexial's existing software and store process information.

Flexial will handle programming and integration, reducing the need for outside labor.

| Equipment / Service | Total ($) |
|---|---:|
| Communication Hardware | 700 |
| Data Storage / Configuration | 500 |
| Integration Testing Materials | 300 |
| Software / License Allowance | 500 |
| **Flexnet / Epicor Subtotal** | **2,000** |

## 6. Overall Project Budget

| Subsystem | Estimated Cost ($) |
|---|---:|
| Cleaning Sensors | 7,000 |
| Passivation Sensors | 17,000 |
| PLC Hardware and Controls | 18,000 |
| Barcode Scanning | 1,000 |
| Flexnet / Epicor Communication | 2,000 |
| **Subtotal** | **45,000** |
| Contingency | 4,500 |
| **Total Estimated Budget** | **49,500** |

## 7. Budget Updates

The current estimated budget for the Flexial PLC Programming and Process Controls project is **$49,500**, which is within the original $50,000 budget limit.

The estimated costs are based on the equipment requirements identified in the cleaning and passivation I/O tables. Prices are preliminary planning estimates and have not yet been confirmed through supplier quotations.

Team 7 will continue researching equipment and comparing prices to ensure the selected components meet Flexial's requirements while staying within the project budget.

The budget may change as equipment is selected and additional information becomes available. Particular attention will be given to sensor compatibility, PLC input/output requirements, and the equipment needed for automatic draining and reconcentration during passivation.


## Division of Labor

### Cleaning Sensors

-Nate Wiser

### Passivation Sensors

-James Tyler

### PLC Hardware and Controls

-Phillip Zarichansky

### Barcode Scanner

-George Songer

### Network Communication

-Izaiah Townsend

### Timeline

Revise the detailed timeline (Gantt chart) you created in the project proposal. Ensure that the timeline is optimized for detailed design. Address critical unknowns early and determine if a prototype needs to be constructed before the final build to validate a subsystem. Additionally, if subsystem $A$ imposes constraints on subsystem $B$, generally, subsystem $A$ should be designed first.


## References

[1] Flexial Corporation, "Operations and Capabilities." [Online]. Available: https://flexial.com/capabilities/

## Statement of Contributions

Each team member is required to make a meaningful contribution to the project proposal. In this section, each team member is required to document their individual contributions to the report. One team member may not record another member's contributions on their behalf. By submitting, the team certifies that each member's statement of contributions is accurate.

