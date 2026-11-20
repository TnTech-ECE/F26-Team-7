
# Project Proposal

## Introduction

Modern manufacturing processes demand precise control, consistent operating conditions, and reliable monitoring systems to ensure product quality and operational efficiency. These requirements are particularly critical in sectors such as aerospace and defense, where manufacturing defects may result in severe consequences. Flexial Corporation manufactures precision metal bellows, accumulators, and flexible metal hose assemblies for aerospace, defense, and other industrial applications. The company also conducts precision cleaning operations for components that must meet stringent cleanliness standards [1]. Consistent processing conditions throughout these operations are essential for producing reliable components that fulfill customer requirements.

To address challenges in monitoring and controlling manufacturing equipment, the senior design team is developing an automation system for Flexial based on a programmable logic controller (PLC). The proposed system will integrate chemical tank monitoring, temperature regulation, valve operation, and process identification within a centralized control framework. Utilizing industrial sensors, a PLC, and a human-machine interface (HMI), the system will provide operators with real-time access to process conditions and enable automated execution of selected operations. The project will also explore the integration of barcode scanning and manufacturing data collection to enhance traceability throughout the production process. These enhancements are intended to reduce manual intervention, improve process consistency, and increase manufacturing efficiency.

This proposal outlines the background of the manufacturing process and identifies the technical challenges associated with implementing an automated control system. A review of existing industrial automation solutions will evaluate available controllers, sensors, and communication technologies to inform the system design. Subsequently, the proposal will define system specifications and constraints, establish measurable success criteria, and detail the resources necessary for implementation, including equipment costs, personnel, and a project timeline. Finally, the proposal will address the specific benefits for Flexial and broader implications of industrial automation, such as safety considerations and professional engineering responsibilities.

## Formulating the Problem

### Problem Statement

Flexial Corporation's cleaning, pickling, and passivation operations require consistent monitoring of process conditions, accurate processing times, and reliable documentation to maintain product quality and traceability. Coordinating these requirements across multiple chemical tanks, sensors, and processing stations presents challenges in monitoring operating conditions, identifying deviations from established requirements, and maintaining accurate records for individual parts. A successful solution must track parts throughout their required processing steps, record relevant process measurements and cycle times, notify operators of abnormal conditions, and demonstrate reliable operation through at least 20 consecutive test cycles without a programming-related failure. 

### Background

Flexial Corporation produces specialized metal components for applications that demand high levels of precision, reliability, and cleanliness. The company's manufacturing capabilities encompass precision machining, welding, testing, and precision cleaning. These processes enable the production of components for aerospace, medical, defense, and other demanding industries [1]. Given that finished products may be deployed in critical applications, it is essential to maintain manufacturing conditions that ensure components meet stringent quality standards.

This project focuses on a manufacturing operation that utilizes multiple chemical processing tanks and associated equipment requiring comprehensive monitoring and control. Key process variables include temperature, pH, chemical concentration, and total dissolved solids (TDS). Monitoring these parameters is critical for detecting changes in solution conditions that could impact processing consistency. Beyond the chemical tanks, the operation also incorporates a drying oven that necessitates temperature monitoring and control. The system must further accommodate equipment such as heaters, valves, stack lights, and operator input devices.

A primary challenge in automating this process is managing the diverse range of electrical and measurement signals required by the equipment. Industrial sensors often generate analog measurements, whereas devices such as valves and relays typically operate with discrete control signals. For instance, pH measurement necessitates an appropriate sensor and transmitter to convert the measurement into a signal interpretable by the control system. Commercial industrial transmitters commonly utilize standardized signals such as 4–20 mA, which are compatible with PLC analog input modules [2]. Integrating these devices demands careful evaluation of electrical compatibility, sensor accuracy, and the control capabilities of the selected hardware.

A programmable logic controller (PLC) provides a potential solution by integrating multiple sensors and actuators within a centralized control system. PLCs are industrial computers engineered to monitor input signals, execute programmed control logic, and operate connected equipment. Their capacity to coordinate industrial machinery renders them suitable for applications that require both continuous monitoring and sequential operations [3]. A properly selected PLC can monitor chemical tank conditions, regulate heating equipment, and coordinate valve operation in accordance with the required manufacturing sequence.

The proposed system will incorporate a human-machine interface (HMI) to provide operators with an accessible platform for monitoring and interacting with equipment. The HMI will display measured process variables, equipment operating conditions, and alarm notifications, while enabling authorized personnel to initiate or modify selected operations. This centralized interface will facilitate access to manufacturing information and minimize the need for direct interaction with individual devices across the system.

Another critical consideration is the collection and management of manufacturing data. Identifying individual components or production batches is essential for maintaining accurate process records and ensuring product traceability. The proposed project will implement barcode scanning to identify parts or jobs and associate them with relevant manufacturing information. Additionally, the system will integrate with Flexial’s existing FlexNet and Epicor software platforms. Establishing communication between manufacturing equipment and these systems will reduce manual data entry and enhance access to production records.

Developing a system with these capabilities presents challenges beyond those addressed by selecting a commercially available controller. The design must accommodate existing equipment, establish reliable communication among diverse instrumentation, and implement robust control logic. Each connected device must be evaluated to determine its electrical requirements, communication protocols, and compatibility with the proposed PLC. Furthermore, the system must address operational safety by implementing appropriate responses to equipment faults, abnormal process conditions, and operator commands. These challenges are interconnected because sensor compatibility and measurement accuracy influence PLC input requirements, while communication reliability and control logic determine how accurately process conditions can be monitored, recorded, and communicated to operators.

Addressing these challenges necessitates a coordinated engineering effort encompassing industrial instrumentation, electrical circuit design, control systems, PLC programming, and software integration. The senior design team will investigate compatible technologies, develop the control architecture, implement the necessary interfaces, and verify system operation. By integrating these engineering disciplines, the project seeks to deliver a practical automation system that fulfills Flexial’s manufacturing requirements and accommodates future enhancements and expansion.

### Stakeholders and Their Needs

| Flexial Management | Consistent production quality and efficient operations |
| --- | --- |
| Machine operators | Clear process status, timers, and alarms |
| Customers | Traceable process records, and accurate components |
| Maintenance Technicians  | Accessible Diagnostics and replacable components |
| IT personnel  | Secure integration with FlexNet and Epicor |
| Safety personnel | Appropriate safeguards around chemical operations |

## Specifications and Constraints

F3PC has consulted with the client and has developed preliminary specifications and constraints for the design of the PLC system.

### Universal Specifications:

- The system shall track when a part enters and exits a specific process by being scanned in and out using a barcode scanning system.
- The system shall keep track of each step of a process a part was in and how long each part took. For example, it will keep track how long a part was in a tank before being moved to the next step of a process.
- The system shall turn on a light above each tank or station when the required amount of time a part has to be in a specific step is met to notify when it is ready for the next step.
- The system shall validate if a part has successfully met the requirements of each specific process it goes through (For example, before and after cleaing, then again for passivation). For cleaning, this is done by ensuring each part has been in each station for the required amount of time and that all the stations were set to the correct range. For passivation, this is done by measuring the thickness of the part before and after the process. If a part is found to not meet the standards when finished with a process, it is flagged as incomplete.
- The system shall communicate the data read and converted from the sensors and PLC to the Flexnet and Epicor software to allow the data to be viewed remotely.
- The system shall not allow remote users to manipulate or change the data found in any way, only allowing for a read-only view.
- The system shall digitally store the data collected for a part and keep the data for a specific part together with its ID number for easy retreval.
  
### Cleaning Process Specifications:

- The system shall read values from the sensors in tank 1 (wash tank) using a 4-20mA current loop output to receive the raw data from the pH, concentration, Total Dissolved Solids (TDS), and temperature to be converted to the proper values.  A drain and fill valve will also be implemented to regulate liquids.
- The system shall read the value of the flow sensor for tank 2 (Air-Blow tank) using a 4-20mA current loop output to receive the raw data and convert it to air flow in PSI.
- The system shall read values from the sensors in tank 3 (city water rinse) using a 4-20mA current loop output to receive the raw data from the pH, TDS, water flow, and temperature to be converted to the proper values. A drain and fill valve will also be implemented to regulate liquids.
- The system shall read values from the sensors in tank 4 (conductive rinse) using a 4-20mA current loop output to receive the raw data from the pH, conductivity, and TDS to be converted to the proper values. A drain and fill valve will also be implemented to regulate liquids in tank. 
- The system shall ensure that the conductivity of tank 4 will remain under 20 Siemens by reading the values from the conductivity sensor and comparing the found conductivity to the desired value.
- The system shall read temperature of the drying ovens while a part is in them.
  
### Passivation Specifications:

- The system shall read values from the sensors in tanks 1, 2, and 3 (Nitric acid tanks) using a 4-20mA current loop output to receive the raw data from the pH, Temperature, TDS, and Concentration independently to be converted to the proper values. A drain and fill valve will also be implemented to regulate liquids in tank. 
- The system shall read values from the sensors in the pickling tank (Nitric acid/Hydrofluoric acid mix) using a 4-20mA current loop output to receive the raw data from the Temperature, TDS, and Concentration to be converted to the proper values.
- The system may be able to read the difference in concentration of the Nitric acid and the Hydroflouric acid in the pickling tank by reading the values from two concentration sensors using a 4-20mA current output.
- The system shall read values from the sensors in the two immersion tanks using a 4-20mA current loop output to receive the raw data from the TDS, Temperature, Concentration, and pH independently to be converted to the proper values.
- The system shall read the value of the water flow sensor of the hose in the manual rinse tank and use its 4-20mA current loop output to convert the value to percent output.
  
### Constraints:

 - The system shall use sensors that have a 4-20 mA current loopp output, which will be converted into a digital output that can be read by the PLC
- The system shall be able to have physical and electrical parts that can be replaced if sensors, probes, or other mechanisms are damaged or unresponsive.
- The system shall be modular in design such that the system logic, hardware, data mapping, and all other design choices allow for additional steps and processes of the part fabrication process to be added to the system, such as heat treating and welding. This requires the PLC to have enough CPU to ensure that there will be enough room for the whole process and that all connections are made such that more connections can be added later.
- The system shall follow the standard IEC 61131-3 for PLC programming. This standard ensures that data from 4-20mA sensors are stored as REAL data types and that the PLC code is modular with each step and process having isolated architecture [4].
- The system shall follow the standards IEC 62443-3-3 and 62443-4-2 for cybersecurity. These standards ensure that the physical PLC, HMI, and sensors are in controlled security zones, that the remote viewing server is in a DMZ zone, and that communication from the viewer and the PLC goes through a firewall before communicating [5].
- The system shall follow the standard NFPA 496 for physical PLC safety. This standard ensures that the electronic panel has a vapor seal to protect it from acidic gases and liquids, that a mechanical air-purge regulator keeps it dry and clean, and that a pressure-differential sensor alerts when water is detercted in the cabinet.
- The system shall follow the standards NEC Article 430 & Article 500 for electrical safety. These standards ensures that grounded steel barries separate the 4-20mA sensor terminal blocks from the 120 VAC high-voltage and that all input and output hardware is protected by running all components through isolated interposing relays with RC snubber circuits to suppress voltage spikes.
- This system shall follow the standards ASTM A967 / AMS 2700  for passivation. These standards ensure that the PLC data or logic cannot be overwritten by operators or supervisors by hardcoding pass and fail calculations into the PLC memory as non-volatile constants and that the data setting process completion to true cannot be pushed to Flexnet or Epicor until the data is confirmed by the endpoints and calculations.


## Survey of Existing Solutions           

Existing industrial automation solutions use programmable logic controllers (PLCs), barcode identification, and manufacturing software to connect production equipment and monitor workflow. Three solutions were researched to evaluate different approaches to integrating manufacturing stations, tracking production, and communicating with higher-level software.

### **Ariens Manufacturing Integration Using PLCs and Ignition**

Ariens a manufacturer of outdoor power equipment, implemented an integrated manufacturing system using PLCs, barcode scanners, and Ignition industrial automation software. The system connects 116 Horner XL7 PLCs to manufacturing equipment, including welding stations, laser cutters, and assembly areas. Operators scan barcodes associated with work orders, allowing the system to retrieve production information from the company's enterprise resource planning (ERP) software. The PLCs collect production data, which is monitored through Ignition and transferred back to the ERP system one.

A major advantage of this solution is its ability to connect independent manufacturing stations while reducing manual data entry and improving production tracking. However, it requires reliable communication between multiple controllers and software systems. This approach closely resembles Flexial's project because it demonstrates how barcode scanning and PLC communication can be used to track manufacturing progress across different workstations.

### **Epicor Advanced Manufacturing Execution System**

Epicor Advanced Manufacturing Execution System (MES) is a commercial software platform used to monitor production activity, collect manufacturing data, and provide real-time visibility into shop-floor operations. The system gathers information from manufacturing equipment and operators to monitor production performance, equipment conditions, and quality. Its data exchange capabilities also allow manufacturing information to be shared with other business systems [7], [8].

An advantage of Epicor Advanced MES is its ability to organize production information in a centralized system. However, it does not replace the need for PLCs to control physical equipment and may require additional software integration and licensing. Since Flexial already uses Epicor, this solution is particularly relevant for understanding how production information could be collected from individual stations and made available throughout the manufacturing process. The team must first determine which Epicor capabilities Flexial currently has available.

### **Beckhoff PC-Based Automation Using TwinCAT**

Beckhoff Automation offers an alternative to conventional PLC hardware through industrial PCs running TwinCAT real-time control software. TwinCAT supports industrial control programming, equipment communication, and process automation. Beckhoff has also demonstrated communication between TwinCAT-controlled equipment and SAP manufacturing software using OPC Unified Architecture (OPC UA), allowing manufacturing information to be exchanged between the control system and higher-level software [9], [10].

The main advantage of this solution is its flexibility in combining machine control and software communication through a PC-based platform. However, it requires specialized hardware, software knowledge, and additional integration work when connecting existing equipment. Although Flexial's project focuses on PLC-based control, Beckhoff demonstrates that similar manufacturing integration can be achieved without relying exclusively on conventional PLC hardware.


# Measures of Success

Team 7 will evaluate the success of the Flexial PLC Programming and Process Controls project based on four main factors: **accuracy, reliability, usability and accessibility, and cost-effectiveness.** These factors will help determine how well the PLC system performs, how easily operators can use it, and how effectively it can be implemented into Flexial's existing processes.

## Accuracy

- **The system's ability to correctly perform the required operations for each department.**
  - The ControlLogix 5580 PLC shall be programmed using ladder logic to control the assigned processes.
  - All inputs and outputs (I/O) shall be identified and tested to ensure they respond correctly.
  - The PLC shall complete the required sequence of operations in the correct order without programming errors.
  - The PLC shall communicate with the Compact 5000 remote I/O to receive sensor readings and control connected equipment.

- **The system's ability to accurately monitor tank conditions.**
  - The system shall include 12 pH measurement points:
    - Two chemical tanks with a nominal pH of 9.0 and a range of 9.0–12.0.
    - Four water rinse tanks with a target pH of 7.0 ±0.1.
    - Six acidic tanks with a pH range of 1.0–3.0, including four acid tanks, one Brite Dip tank, and one Citric tank.
  - The selected pH sensors shall meet the proposed accuracy requirement of ±0.05–0.1 pH units, subject to verification.
  - Six temperature sensors shall be used, including two in Cleaning and four in Passivation.
  - Six concentration or titration measurements shall be included:
    - Two Cleaning chemical measurements at 1–2%.
    - One combined hydrofluoric/nitric acid measurement at F1.
    - Three nitric acid measurements at F2, F3, and F4.
  - Conductivity/TDS shall be monitored at R3.
  - Sensors shall be selected based on accuracy, chemical compatibility, and compatibility with the PLC's 4–20 mA input system.
  - The PLC shall identify readings outside the approved operating ranges and provide an appropriate warning or alarm.

- **The system's ability to communicate with Flexial's existing software.**
  - The PLC shall be configured to communicate with FlexNet and Epicor using compatible communication methods.
  - Information transferred between the PLC and other systems shall be checked to ensure the correct data is received.
  - Each programmed process shall be tested multiple times to verify consistent operation.

## Reliability

- **The system's ability to operate safely and consistently during normal production.**
  - The PLC shall be capable of operating for extended periods without unexpected interruptions caused by programming errors.
  - Safety features shall be included to prevent equipment from operating under unsafe conditions.
  - The system shall recognize incorrect operating conditions and respond according to the approved safety procedures.
  - Each process shall successfully complete at least 20 consecutive test cycles without a programming-related failure.

- **The system's ability to monitor process timing.**
  - A process timing Add-On Instruction (AOI) shall be developed for each tank or oven requiring time monitoring.
  - The AOI shall accept Set Time, Reset, Start, Warn Time, and Alarm Time as inputs.
  - The AOI shall provide Total Run Time, Remaining Time, OK Status, Warn Status, and Alarm Status as outputs.
  - All time values shall be represented in hours, minutes, and seconds.
  - The system shall display the appropriate status when the configured warning or alarm time is reached.

- **The system's ability to handle unexpected problems.**
  - The PLC shall respond safely to power loss, communication errors, sensor failures, and other possible faults.
  - The system shall provide fault indicators to help operators identify problems.
  - Automatic chemical-handling operations shall require approved safety conditions before being performed.
  - The system shall be tested to verify that it responds correctly to simulated fault conditions.

## Usability and Accessibility

- **The system's ability to be easily operated by Flexial employees.**
  - A user interface shall be developed to allow operators to control and monitor the process.
  - The interface shall provide clear instructions to guide operators through each step.
  - Operators shall be able to view current sensor readings, process status, remaining time, and active alarms.
  - The system shall include features that help reduce human errors during operation.

- **The system's ability to track process information.**
  - Operators shall be able to scan a part number before beginning a process.
  - The system shall associate the part number with the recorded process information.
  - Recorded information shall include relevant sensor readings, process times, and alarms.
  - The required data storage period and retrieval method shall be confirmed with Flexial.

- **The system's ability to be maintained and modified when needed.**
  - Team 7 shall provide documentation of the PLC programs, hardware requirements, and I/O connections.
  - PLC programs shall be organized to make troubleshooting and future changes easier.
  - The required hardware and software shall be identified so replacement components can be obtained when needed.

- **The system's ability to support employee training.**
  - A training procedure shall be developed to explain how to operate the system.
  - Operators shall be able to follow the instructions provided through the user interface to complete the process.

## Cost-Effectiveness

- **The system's ability to provide an affordable solution for improving Flexial's production processes.**
  - Team 7 shall create a list of the hardware and software needed to implement the PLC system.
  - The total estimated cost of the equipment and implementation shall be documented.
  - The proposed system shall be evaluated against Flexial's estimated project budget of $40,000–$50,000.
  - Existing equipment shall be used whenever possible to reduce additional expenses.
  - Three sensor options shall be researched for each required sensor application, comparing accuracy, 4–20 mA compatibility, cost, manufacturer, and purchasing source.
  - A phased implementation plan shall outline the expected costs and time required for each stage of the project.

## Testing Methodology

### Accuracy

- Test each PLC program to ensure the ladder logic performs the correct sequence of operations.
- Check all inputs and outputs individually for proper functionality.
- Compare sensor readings with calibrated reference measurements to verify accuracy.
- Test the pH monitoring system against the required ranges and accuracy specifications.
- Simulate out-of-range sensor readings to verify that the correct warnings and alarms are displayed.
- Test communication with FlexNet and Epicor when the necessary connections are available.

### Reliability

- Test each process for at least 20 consecutive cycles without a programming-related failure.
- Verify that the timing AOI correctly calculates total runtime and remaining time.
- Test the AOI's OK, warning, and alarm outputs using configured time values.
- Test fault detection by simulating sensor failures, communication interruptions, and other applicable errors.
- Verify that the PLC responds according to the approved safety procedures.

### Usability

- Test the user interface to confirm operators can start, stop, and monitor the process.
- Verify that sensor readings, process times, and alarms are displayed correctly.
- Test barcode scanning to confirm that the correct part number is associated with recorded process data.
- Demonstrate the training procedure to evaluate whether an operator can follow the instructions.
- Demonstrate how the PLC program can be adjusted or troubleshot when necessary.

### Cost-Effectiveness

- Compare the estimated equipment and implementation costs with the available project budget.
- Evaluate three sensor options for each required application based on accuracy, compatibility, price, and availability.
- Review the phased implementation plan to determine whether the proposed timeline and expenses are reasonable.
- Update the budget as final equipment selections and vendor pricing become available.


# Resources

Team 7 will need hardware, software, personnel, and documentation to complete the Flexial PLC Programming and Process Controls project. Flexial has provided the initial PLC architecture and sensor requirements. Since the project is divided into three phases, some equipment and responsibilities are still being determined.

## Hardware

- **PLC:** Allen-Bradley ControlLogix 5580, used as the main controller for the system.
- **Remote I/O:** Compact 5000 remote I/O, used to connect sensors and other equipment to the PLC.
- **PLC Processor:** Executes the ladder logic programs and controls the assigned processes.
- **Memory:** Stores PLC programs and system information.
- **Power Supply:** Provides power to the PLC, remote I/O, and connected components.
- **pH Sensors:** Twelve measurement points:
  - Two chemical tanks with a nominal pH of 9.0 and a range of 9.0–12.0.
  - Four water rinse tanks with a target pH of 7.0 ±0.1.
  - Six acidic tanks with a pH range of 1.0–3.0, including four acid tanks, one Brite Dip tank, and one Citric tank.
- **Temperature Sensors:** Six measurement points, including two in Cleaning and four in Passivation. Thermocouples in protective stainless-steel tubes or RTDs are being considered.
- **Concentration/Titration Meters:** Six measurement applications:
  - Two Cleaning chemical measurements at 1–2%.
  - One combined hydrofluoric/nitric acid measurement at F1.
  - Three nitric acid measurements at F2, F3, and F4.
- **Conductivity/TDS Meter:** One measurement point at R3.
- **Additional Measurement Equipment:** An oven dry sensor, passivation/pickling oxide film sensor, and before/after weight measurement equipment are being considered.
- **Input/Output Modules:** Connect sensors, valves, indicators, and other equipment to the PLC.
- **Control Panel and Wiring:** Includes the enclosure, terminal blocks, wiring, and other components needed to connect the system.

## PLC I/O Requirements

The current sensor requirements identify 25 measurement points:

- 12 pH measurements.
- 6 temperature measurements.
- 6 concentration/titration measurements.
- 1 conductivity/TDS measurement.

Additional measurements may be required for the oven, oxide film, and before/after weight measurements.

The final number of analog and digital I/O channels will be determined after the sensor types and signal interfaces are selected. The team will also consider approximately 20% additional I/O capacity for future expansion.

The power supply requirements will be determined using the selected PLC hardware, instrumentation, and connected equipment.

## Sensor Selection

Team 7 will research three options for each required sensor application.

Each option will be compared based on:

- Measurement accuracy.
- Compatibility with 4–20 mA PLC signals.
- Cost.
- Manufacturer or brand.
- Purchasing source.
- Compatibility with the chemicals and operating conditions.

The final selections will be reviewed with Flexial before equipment is purchased.

## Software

- **PLC Programming Software:** Used to develop, test, and modify ladder logic programs and the required Add-On Instructions.
- **FlexNet:** Flexial's existing software that the PLC system will need to communicate with.
- **Epicor:** Flexial's existing system that may need to exchange process information with the PLC system.
- **User Interface Software:** Allows operators to monitor sensor readings, process times, alarms, and equipment status.

## Personnel

- **Team 7:** Responsible for equipment research, proposed PLC programming, testing, and project documentation.
- **Flexial Employees:** Provide information about existing equipment, manufacturing processes, and operating requirements.
- **Project Supervisor:** Provides guidance and feedback throughout the project.
- **Flexial Technical Personnel:** Assist with equipment selection, software integration requirements, and safety reviews.

The final responsibilities for PLC programming, installation, and FlexNet/Epicor integration will be confirmed with Flexial, but are unknown at this time.

## Documentation

- PLC programming manuals.
- ControlLogix 5580 and Compact 5000 remote I/O documentation.
- Sensor datasheets and equipment specifications.
- Wiring diagrams and I/O connection lists.
- Flexial's existing process information.
- Process timing Add-On Instruction (AOI) documentation.
- Project budget and timeline.
- Testing procedures and results.


## Resource Availability

Flexial has specified a ControlLogix 5580 PLC communicating with Compact 5000 remote I/O. The initial setup is estimated at approximately $22,000.

The overall project budget is estimated to be between $40,000 and $50,000. Since the project is divided into three phases, equipment quantities and costs will be updated as additional requirements are confirmed with Flexial.

Final sensor selections, I/O module quantities, and software integration responsibilities are still being determined.


### **Personel**

**Required Skills**

The Flexial PLC Programming and Process Controls project requires knowledge of programmable logic controllers (PLCs), industrial automation, electrical hardware, embedded systems, computer programming, and communication networks. The main objective of this project is to develop an integrated PLC-based control system that connects and coordinates the manufacturing processes throughout Flexial's facility. To accomplish this, the team must understand PLC ladder logic, input/output (I/O) configurations, process control, and the communication methods needed to connect the PLC system with Flexial's existing FlexNet and Epicor software.

**Team Skills**

The team consists of five engineering students with backgrounds in power engineering, control systems, and embedded systems. Each team member brings different technical skills and experience that will contribute to the successful development of the project.

- Nate: C, C++, Assembly, Microsoft Excel, soldering, and SCADA systems. Nate has completed more power engineering courses at Tennessee Tech than the other team members, providing a strong background in electrical power systems and related equipment.
- James: C, C++, Assembly, soldering, PLC ladder logic, and PLC Fiddle. James has a background in both power engineering and control systems, providing experience relevant to PLC programming and electrical hardware.
- Philip: C, C++, Assembly, PLC ladder logic, and PLC Fiddle. Philip has experience working with PLCs through coursework at Tennessee Tech as well as previous experience from high school. He currently has the most hands-on PLC experience among the team members.
- George: C, C++, Assembly, and PLC Fiddle. George has a background in control systems and programming, which will be useful when developing and testing PLC logic.
- Izaiah: C, C++, Assembly, communications, computer programming, and hardware experience. His background will be particularly valuable for the embedded systems and communication portions of the project, especially when connecting the PLC system with Flexial's existing network and software.

The combined skills of the team provide a foundation for completing the PLC programming, hardware integration, and communication requirements of the project. Two team members have completed the PLC course offered at Tennessee Tech, while another is currently taking the course. The remaining two members plan to take the course in a future semester. This allows the team to use its existing PLC experience while continuing to develop the additional knowledge needed for the project.

### **Skill Gaps and Development Plan**

One of the team's main skill gaps is the lack of experience with embedded systems and industrial communication networks. Nate, James, Philip, and George have limited knowledge in these areas, which may present challenges when connecting the PLC system to Flexial's existing FlexNet and Epicor software. To address this gap, Izaiah will take the lead on the communication portion of the project, working closely with Mike Abell to understand the required communication protocols and software integration. The remaining team members will stay actively involved and work with Izaiah to develop their knowledge and ensure everyone understands this portion of the project.

Another area requiring improvement is the team's overall PLC knowledge. While several members have completed or are currently enrolled in PLC coursework, not everyone has the same level of experience. Nate and Izaiah, for example, have focused primarily on power engineering and Embedded systems and neither of them have taken a controls course. To help address this knowledge gap, the team has provided them with access to the PLC course materials previously used at Tennessee Tech. Team members with more PLC experience will also be available to answer questions and assist with understanding ladder logic and control-system operation.

As the project progresses, the team will continue developing its knowledge through independent research, manufacturer documentation, hands-on programming, and communication with Flexial's engineers.

**Project Supervisor**

The team has been assigned Kevin Mumpower as its project supervisor through Flexial, the company sponsoring the capstone project. Kevin has extensive knowledge of the overall project, including the manufacturing processes involved and how the different sections of the proposed system are intended to connect.

His understanding of Flexial's operations makes him well suited to supervise the project. He will help the team understand the company's requirements, provide guidance on the overall direction of the project, and assist with coordinating the different portions of the control system. His knowledge will be particularly valuable in ensuring that the proposed PLC system meets Flexial's needs and can be integrated into its existing manufacturing operations.

### **Instructors and Technical Guidance**

The team has two instructors providing technical guidance for the different portions of the project: Ron Scarlett and Mike Abell.

Ron Scarlett will provide guidance primarily for the PLC hardware and software portions of the project. He has many years of experience in PLC programming, hardware installation, and industrial control systems. His experience will be valuable when the team encounters challenges involving ladder logic, hardware selection, wiring, troubleshooting, and the implementation of control sequences. Ron is expected to provide the majority of the team's guidance throughout the PLC development process.

Mike Abell will provide guidance for the communication and networking portions of the project. Mike serves as an IT Manager and has knowledge of the communication protocols, network infrastructure, and internal management software used by Flexial. He also has previous experience with PLC ladder logic programming. His primary role will be assisting with the integration of the PLC system into Flexial's existing communication network and software systems, including FlexNet and Epicor.

During the team's initial meeting with Flexial, it was established that the embedded systems engineer would communicate directly with Mike for much of the project. This communication will be important for determining how information will be transferred between the PLC system and Flexial's existing software.

Together, Ron Scarlett and Mike Abell will provide the technical guidance necessary to address both the PLC controls and communication requirements of the project. Their combined experience will help the team develop a functional, integrated system that meets the objectives established by Flexial.

### Timeline

<img width="1827" height="743" alt="image" src="https://github.com/user-attachments/assets/4ca85fc6-db8d-4bf8-9c30-9b7f864c9b44" />


# Specific Implications

## **Ethical, Professional, and Standards Considerations**

There are a multitude of reasons for the PLC to be put into place within the company. There are many workers that interact with dangerous chemicals and potential hazards, the automation of the process will provide a safer work environment for employees. The PLC will also have the intention in reducing errors that can be made by people, making sure that everything that interacts with it is consistent. A better consistency will also allow for more money to be saved by having less product incorrectly handled, resulting in less waste. The speed of the process should also be faster, having a machine that can process more materials than the average worker can handle with the same quality.
A broader implication that can be taken from this machine is the fact that reducing waste also helps lessen pollution being added to the environment. If parts are constantly being thrown away then that creates more of a possibility that it affects the environment. There are also workers that are spared from the risk of injury and this not only protects the workers, but also protects the company from dealing with any kind of legal trouble, within proper use of the machine. It is possible that the automation of these processes may remove some of the available jobs for current workers, but it also opens the possibility of them learning to handle machinery or be moved into an arguably better position. Every project also has to consider what happens if anything within the machine fails, this risk should be mitigated by having failsafes that will remove/ contain anything that could harm a worker.

## Statement of Contributions

Each team member must contribute meaningfully to the project proposal. In this section, each team member is required to document their individual contributions to the report. One team member may not record another member's contributions on their behalf. By submitting, the team certifies that each member's statement of contributions is accurate.

James: Personal section, Survey of existing solutions section.

George: Specifications, Constraints, Gantt Chart.

Phillip: Introduction, Background, Stakeholders, Problem Statement.

Izaiah: Specific & Broader implications.

Nate: Measure of Success, Budget, Resources.




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


# Operational Flow Chart

## Cleaning Subsystem

<img width="2670" height="3092" alt="image" src="https://github.com/user-attachments/assets/b29b278e-1e26-407b-b4e0-da79d0d550b5" />


## Passivation Subsystem

<img width="3952" height="3130" alt="image" src="https://github.com/user-attachments/assets/086efbde-2df4-443a-8894-e00a3c8399c9" />


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


# Budget

## Project Budget Overview

Team 7 has an estimated budget of **$40,000–$50,000** for the Flexial PLC Programming and Process Controls project.

The budget is divided into five subsystems: cleaning sensors, passivation sensors, PLC hardware and controls, barcode scanning, and FlexNet/Epicor communication.

Flexial has specified a ControlLogix 5580 PLC with Compact 5000 remote I/O. The initial PLC setup is estimated at approximately $22,000.

The following budget is a preliminary planning estimate based on the latest equipment requirements and previously estimated prices. Final costs will be determined after equipment selections and vendor quotes are received.

## 1. Cleaning Sensors

This subsystem includes the sensors needed to monitor the cleaning tanks and chemical conditions.

| Equipment | Quantity | Unit Price ($) | Total ($) |
|---|---:|---:|---:|
| pH Sensors | 6 | 500 | 3,000 |
| Temperature Sensors | 2 | 150 | 300 |
| Concentration Sensors | 2 | 1,500 | 3,000 |
| Water Flow Sensor | 1 | 400 | 400 |
| Air Flow Measurements | 2 | 500 | 1,000 |
| **Cleaning Subtotal** | | | **7,700** |

The sensor quantities reflect the current cleaning requirements where the department assignment is identified. Flow measurements remain preliminary and will be confirmed with Flexial.

## 2. Passivation Sensors

This subsystem includes sensors used to monitor the passivation tanks and chemical conditions.

| Equipment | Quantity | Unit Price ($) | Total ($) |
|---|---:|---:|---:|
| pH Sensors | 6 | 500 | 3,000 |
| Temperature Sensors | 4 | 150 | 600 |
| Concentration Sensors | 4 | 1,500 | 6,000 |
| Conductivity/TDS Sensor | 1 | 500 | 500 |
| Water Flow Sensor | 1 | 400 | 400 |
| **Passivation Subtotal** | | | **10,500** |

Additional measurement equipment, including oxide film measurement and before/after weight measurement devices, is being considered but has not been included in the current subtotal.

## 3. PLC Hardware and Controls

This subsystem includes the main PLC equipment, remote I/O, user interface, valves, and other control components.

| Equipment | Quantity | Estimated Total ($) |
|---|---:|---:|
| ControlLogix 5580 PLC and Compact 5000 Remote I/O Initial Setup | 1 | 22,000 |
| User Interface | 1 | 1,500 |
| Fill Valves | 6 | 1,800 |
| Drain Valves | 6 | 1,800 |
| Control Cabinet and Wiring | 1 | 2,000 |
| Safety Equipment / Relays | TBD | 1,300 |
| **PLC Subtotal** | | **30,400** |

The $22,000 initial setup estimate was provided by Flexial. The components included in this estimate must be confirmed to avoid double-counting PLC hardware, I/O modules, power supplies, or network equipment.

The valve prices are preliminary estimates of $300 per valve. Final valve selections must be compatible with the chemicals used in the cleaning and passivation processes, including nitric and hydrofluoric acid where applicable.

## 4. Barcode Scanning

This subsystem will allow operators to scan part numbers and associate them with recorded process information.

| Equipment | Quantity | Total ($) |
|---|---:|---:|
| Barcode Scanner | 1 | 650 |
| Scanner Communication Hardware | 1 | 200 |
| Part Number Storage Setup | 1 | 150 |
| **Barcode Subtotal** | | **1,000** |

## 5. FlexNet / Epicor Communication

This subsystem will allow the PLC system to communicate with Flexial's existing software and store process information.

Programming and software integration responsibilities will be confirmed with Flexial.

| Equipment / Service | Total ($) |
|---|---:|
| Communication Hardware | 700 |
| Data Storage / Configuration | 500 |
| Integration Testing Materials | 300 |
| Software / License Allowance | 500 |
| **FlexNet / Epicor Subtotal** | **2,000** |

These costs are preliminary allowances. Existing software and communication equipment may reduce the amount of additional hardware required.

## 6. Overall Project Budget

| Subsystem | Estimated Cost ($) |
|---|---:|
| Cleaning Sensors | 7,700 |
| Passivation Sensors | 10,500 |
| PLC Hardware and Controls | 30,400 |
| Barcode Scanning | 1,000 |
| FlexNet / Epicor Communication | 2,000 |
| **Subtotal** | **51,600** |
| Contingency (10%) | 5,160 |
| **Total Estimated Budget** | **56,760** |
| **Maximum Project Budget** | **50,000** |
| **Amount Over Budget** | **6,760** |

The current revised estimate exceeds the $50,000 budget limit by $6,760.

This estimate is not final. Equipment quantities, PLC setup costs, and vendor pricing must be confirmed before the budget can be finalized.

## 7. Budget Updates

The original project estimate was $49,500, including a 10% contingency. The revised estimate reflects the updated sensor quantities and the approximately $22,000 PLC setup cost provided by Flexial.

### Sensor Selection

Team 7 will research three options for each required sensor application. The options will be compared based on:

- Accuracy.
- 4–20 mA PLC compatibility.
- Chemical compatibility.
- Cost.
- Manufacturer.
- Purchasing source.

The latest requirements identify 12 pH measurement points, six temperature measurements, six concentration/titration measurements, and one conductivity/TDS measurement.

### PLC Equipment

The ControlLogix 5580 PLC and Compact 5000 remote I/O will be used for the system.

The final number of analog and digital I/O modules will be determined after the equipment requirements are confirmed. Approximately 20% additional I/O capacity will be considered for future expansion.

### Valve Pricing

The current valve prices are preliminary estimates. Team 7 will obtain pricing for chemical-resistant actuated valves that meet Flexial's operating requirements.

### Cost Reduction

To remain within the $50,000 project budget, Team 7 will review equipment costs with Flexial and identify possible cost reductions.

Possible adjustments include:

- Using existing equipment when available.
- Comparing lower-cost sensor options that meet the required specifications.
- Confirming which components are included in the $22,000 PLC setup.
- Purchasing equipment in phases based on project priorities.

The budget will be updated as final equipment selections and vendor quotes become available.


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


## References


[1] Flexial Corporation, "Operations and Capabilities." [Online]. Available: https://flexial.com/capabilities/

[2] Endress+Hauser, "Liquiline M CM42 — Transmitter for pH/ORP, Conductivity, and Oxygen." [Online]. Available: https://www.endress.com/en/field-instruments-overview/liquid-analysis-product-overview/ex-approved-transmitter-cm42

[3] Rockwell Automation, "Programmable Controllers." [Online]. Available: https://www.rockwellautomation.com/en-us/products/hardware/programmable-controllers.html

[4]  PLCopen, “PLCopen Standards.” [Online]. Avalible: https://www.plcopen.org/standards/

[5] Fortinet, “**The IEC 62443 Industrial Cybersecurity Standard” [Online]. Available:** https://www.fortinet.com/resources/cyberglossary/iec-62443

[6] Inductive Automation, “New SCADA and OEE for Ariens, Maker of Four Million Snow Blowers,” Inductive Automation, 2021. [Online]. Available:
https://inductiveautomation.com/resources/customerproject/new-scada-and-oee-for-ariens-maker-of-four-million-snow-blowers

[7] Epicor Software Corporation, “Epicor Advanced MES,” Epicor. [Online]. Available:
https://www.epicor.com/en/products/manufacturing-execution-software-mes/advanced-mes/

[8] Epicor Software Corporation, “Epicor Advanced MES Data Exchange,” Epicor. [Online]. Available:
https://www.epicor.com/en-us/products/manufacturing-execution-software-mes/advanced-mes/ptw-data-exchange/

[9] Beckhoff Automation, “TC1200 — TwinCAT 3 PLC,” Beckhoff Automation. [Online]. Available:
https://www.beckhoff.com/en-us/products/automation/twincat/tcxxxx-twincat-3-base/tc1200.html

[10] Beckhoff Automation, “TwinCAT OPC UA to Integrate the Shop Floor with the Top Floor,” technical demonstration, Beckhoff Automation. [Online]. Available:
https://download.beckhoff.com/download/software/twincat/TwinCAT2/Solutions/PLC-ConnectedTo-SAP/OPC-UA-SAP-Beckhoff-v2.pdf

## Statement of Contributions

Each team member is required to make a meaningful contribution to the project proposal. In this section, each team member is required to document their individual contributions to the report. One team member may not record another member's contributions on their behalf. By submitting, the team certifies that each member's statement of contributions is accurate.

Phillip: Introduction, Background, Stakeholders, Problem Statement, and Atomic Subsystems.

Nate: Measure of Success, Budget, Resources, and Flowcharts.

James: Personal section, Survey of existing solutions section, and Hardware Block Diagram.

Izaiah: Specific & Broader implications, and High Level Solution

George: Specifications, Constraints, Gantt Chart, and Atomic Subsystems.
