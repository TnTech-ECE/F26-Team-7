# Conceptual Design

This document outlines the objectives of a conceptual design. After reading your conceptual design, the reader should understand:

- The fully formulated problem.
- The fully decomposed conceptual solution.
- Specifications for each of the atomic pieces of the solution.
- Any additional constraints and their origins.
- How the team will accomplish their goals given the available resources.

With these guidelines, each team is expected to create a suitable document to achieve the intended objectives and effectively inform their stakeholders.


## General Requirements for the Document
- Submissions must be composed in Markdown format. Submitting PDFs or Word documents is not permitted.
- All information that is not considered common knowledge among the audience must be properly cited.
- The document should be written in the third person.
- An introduction section should be included.
- The latest fully formulated problem must be clearly articulated using explicit "shall" statements.
- A comparative analysis of potential solutions must be performed
- The document must present a comprehensive, well-specified high-level solution.
- The solution must contain a hardware block diagram.
- The solution must contain an operational flowchart.
- For every atomic subsystem, a detailed functional description, inputs, outputs, and specifications must be provided.
- The document should include an acknowledgment of ethical, professional, and standards considerations, explaining the specific constraints imposed.
- The solution must include a refined estimate of the resources needed, including: costs, allocation of responsibilities for each subsystem, and a Gantt chart.


## Introduction

Modern manufacturing processes demand precise control, consistent operating conditions, and reliable monitoring systems to ensure product quality and operational efficiency. These requirements are particularly critical in sectors such as aerospace and defense, where manufacturing defects may result in severe consequences. Flexial Corporation manufactures precision metal bellows, accumulators, and flexible metal hose assemblies for aerospace, defense, and other industrial applications. The company also conducts precision cleaning operations for components that must meet stringent cleanliness standards [1]. Consistent processing conditions throughout these operations are essential for producing reliable components that fulfill customer requirements.

To address challenges in monitoring and controlling manufacturing equipment, the senior design team is developing an automation system for Flexial based on a programmable logic controller (PLC). The proposed system will integrate chemical tank monitoring, temperature regulation, valve operation, and process identification within a centralized control framework. Utilizing industrial sensors, a PLC, and a human-machine interface (HMI), the system will provide operators with real-time access to process conditions and enable automated execution of selected operations. The project will also explore the integration of barcode scanning and manufacturing data collection to enhance traceability throughout the production process. These enhancements are intended to reduce manual intervention, improve process consistency, and increase manufacturing efficiency.


## Restating the Fully Formulated Problem

### Background

Flexial Corporation produces specialized metal components for applications that demand high levels of precision, reliability, and cleanliness. The company's manufacturing capabilities encompass precision machining, welding, testing, and precision cleaning. These processes enable the production of components for aerospace, medical, defense, and other demanding industries [1]. Given that finished products may be deployed in critical applications, it is essential to maintain manufacturing conditions that ensure components meet stringent quality standards.

This project focuses on a manufacturing operation that utilizes multiple chemical processing tanks and associated equipment requiring comprehensive monitoring and control. Key process variables include temperature, pH, chemical concentration, and total dissolved solids (TDS). Monitoring these parameters is critical for detecting changes in solution conditions that could impact processing consistency. Beyond the chemical tanks, the operation also incorporates a drying oven that necessitates temperature monitoring and control. The system must further accommodate equipment such as heaters, valves, stack lights, and operator input devices.

A primary challenge in automating this process is managing the diverse range of electrical and measurement signals required by the equipment. Industrial sensors often generate analog measurements, whereas devices such as valves and relays typically operate with discrete control signals. For instance, pH measurement necessitates an appropriate sensor and transmitter to convert the measurement into a signal interpretable by the control system. Commercial industrial transmitters commonly utilize standardized signals such as 4–20 mA, which are compatible with PLC analog input modules [2]. Integrating these devices demands careful evaluation of electrical compatibility, sensor accuracy, and the control capabilities of the selected hardware.

A programmable logic controller (PLC) provides a potential solution by integrating multiple sensors and actuators within a centralized control system. PLCs are industrial computers engineered to monitor input signals, execute programmed control logic, and operate connected equipment. Their capacity to coordinate industrial machinery renders them suitable for applications that require both continuous monitoring and sequential operations [3]. A properly selected PLC can monitor chemical tank conditions, regulate heating equipment, and coordinate valve operation in accordance with the required manufacturing sequence.

The proposed system will incorporate a human-machine interface (HMI) to provide operators with an accessible platform for monitoring and interacting with equipment. The HMI will display measured process variables, equipment operating conditions, and alarm notifications, while enabling authorized personnel to initiate or modify selected operations. This centralized interface will facilitate access to manufacturing information and minimize the need for direct interaction with individual devices across the system.

Another critical consideration is the collection and management of manufacturing data. Identifying individual components or production batches is essential for maintaining accurate process records and ensuring product traceability. The proposed project will implement barcode scanning to identify parts or jobs and associate them with relevant manufacturing information. Additionally, the system will integrate with Flexial’s existing FlexNet and Epicor software platforms. Establishing communication between manufacturing equipment and these systems will reduce manual data entry and enhance access to production records.

Developing a system with these capabilities presents challenges beyond those addressed by selecting a commercially available controller. The design must accommodate existing equipment, establish reliable communication among diverse instrumentation, and implement robust control logic. Each connected device must be evaluated to determine its electrical requirements, communication protocols, and compatibility with the proposed PLC. Furthermore, the system must address operational safety by implementing appropriate responses to equipment faults, abnormal process conditions, and operator commands.

Addressing these challenges necessitates a coordinated engineering effort encompassing industrial instrumentation, electrical circuit design, control systems, PLC programming, and software integration. The senior design team will investigate compatible technologies, develop the control architecture, implement the necessary interfaces, and verify system operation. By integrating these engineering disciplines, the project seeks to deliver a practical automation system that fulfills Flexial’s manufacturing requirements and accommodates future enhancements and expansion.

### Specifications and Constraints

F3PC has consulted with the client and has developed preliminary specifications and constraints for the design of the PLC system.

## Capability Specifications
- The system shall track where a part is in the fabrication process, with our team beginning at the cleaning process.

- The system shall use a barcode system to scan a part in and out of the cleaning process.

- The system shall measure and read values from the hypersonic preclean and cleaning tanks, such as pH, concentration, TDS, and the temperature of the tanks, as well as time in the tanks. 

- The system shall measure the temperature of the drying ovens and the time a part is in the ovens.

- The system shall measure and read values similar to the cleaning tanks for the passivation tanks

- The system shall be able to ensure that a part comes out of cleaning properly and will notify the user if any error is found.

- The system may have more steps of the fabrication process added to it, such as heat treating, forming, and welding.

## Constraints

- The system shall be able to have more operations of the fabrication process added to it.

- The system shall use 4-20mA analog sensors to measure and read values from the cleaning tanks.

- The system shall allow for replacement sensors so if they wear out or are damaged the system does not have to be redone.

- The system shall follow all regulations of logic, motor control, code safety, and all other coding regulations detailed in IEC 61131 [4].

- The system shall follow all electrical, component, and cybersecurity safety regulations detailed in IEC 62443 [5].


## Comparative Analysis of Potential Solutions

In this section, various potential solutions are hypothesized, design considerations are discussed, and factors influencing the selection of a solution are outlined. The chosen solution is then identified with justifications for its selection.


## High-Level Solution

This section presents a comprehensive, high-level solution aimed at efficiently fulfilling all specified requirements and constraints. The solution is designed to maximize stakeholder goal attainment, adhere to established constraints, minimize risks, and optimize resource utilization. Please elaborate on how your design accomplishes these objectives.


### Hardware Block Diagram

Block diagrams are an excellent way to provide an overarching understanding of a system and the relationships among its individual components. Generally, block diagrams draw from visual modeling languages like the Universal Modeling Language (UML). Each block represents a subsystem, and each connection indicates a relationship between the connected blocks. Typically, the relationship in a system diagram denotes an input-output interaction.

In the block diagram, each subsystem should be depicted by a single block. For each block, there should be a brief explanation of its functional expectations and associated constraints. Similarly, each connection should have a concise description of the relationship it represents, including the nature of the connection (such as power, analog signal, serial communication, or wireless communication) and any relevant constraints.

The end result should present a comprehensive view of a well-defined system, delegating all atomic responsibilities necessary to accomplish the project scope to their respective subsystems.

<img width="1776" height="1186" alt="image" src="https://github.com/user-attachments/assets/cec01598-f38d-4a80-8667-938ba793018f" />


### Operational Flow Chart

Similar to a block diagram, the flow chart aims to specify the system, but from the user's point of view rather than illustrating the arrangement of each subsystem. It outlines the steps a user needs to perform to use the device and the screens/interfaces they will encounter. A diagram should be drawn to represent this process. Each step should be represented in the diagram to visually depict the sequence of actions and corresponding screens/interfaces the user will encounter while using the device.


## Atomic Subsystem Specifications

Based on the high-level design, provide a comprehensive description of the functions each subsection will perform.

Inclued a description of the interfaces between this subsystem and other subsystems:
- Give the type of signal (e.g. power, analog signal, serial communication, wireless communication, etc).
- Clearly define the direction of the signal (input or output).
- Document the communication protocols used.
- Specifying what data will be sent and what will be received.

Detail the operation of the subsystem:
- Illustrate the expected user interface, if applicable.
- Include functional flowcharts that capture the major sequential steps needed to achieve the desired functionalities.

For all subsystems, formulate detailed "shall" statements. Ensure these statements are comprehensive enough so that an engineer who is unfamiliar with your project can design the subsystem based on your specifications. Assume the role of the customer in this context to provide clear and precise requirements.



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

###User Interface
The system will run into Optix. This is a way of displaying the HMI style interface onto a server. 

- The subsystem shall give a user friendly way to monitor data points and see that they are recorded.

## Ethical, Professional, and Standards Considerations

In the project proposal, each team must evaluate the broader impacts of the project on culture, society, the environment, public health, public safety, and the economy. Additionally, teams must consider relevant standards organizations that will inform the design process. A comprehensive discussion should be included on how these considerations have influenced the design. This includes detailing constraints, specifications, and practices implemented as a result, and how these address the identified considerations.


## Resources

You have already estimated the resources needed to complete the solution. Now, let's refine those estimates.

### Budget

Develop a budget proposal with justifications for expenses associated with each subsystem. Note that the total of this budget proposal can also serve as a specification for each subsystem. After creating the budgets for individual subsystems, merge them to create a comprehensive budget for the entire solution.

### Division of Labor

First, conduct a thorough analysis of the skills currently available within the team, and then compare these skills to the specific requirements of each subsystem. Based on this analysis, appoint a team member to take the specifications for each subsystem and generate a corresponding solution (i.e. detailed design). If there are more team members than subsystems, consider further subdividing the solutions into smaller tasks or components, thereby allowing each team member the opportunity to design a subsystem.

### Timeline

Revise the detailed timeline (Gantt chart) you created in the project proposal. Ensure that the timeline is optimized for detailed design. Address critical unknowns early and determine if a prototype needs to be constructed before the final build to validate a subsystem. Additionally, if subsystem $A$ imposes constraints on subsystem $B$, generally, subsystem $A$ should be designed first.


## References

[1] Flexial Corporation, "Operations and Capabilities." [Online]. Available: https://flexial.com/capabilities/

## Statement of Contributions

Each team member is required to make a meaningful contribution to the project proposal. In this section, each team member is required to document their individual contributions to the report. One team member may not record another member's contributions on their behalf. By submitting, the team certifies that each member's statement of contributions is accurate.

