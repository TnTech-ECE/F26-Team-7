# Project Proposal

## Introduction

Modern manufacturing processes require precise control, consistant operating conditions, and reliable monitering systems to maintain product quality and efficiency. These requirements are espescially important in industries such as aerospace and defence, where defects can have dire consequences. Flexial Corporation specializes in manufacturing precision metal bellows, accumulators, and flexible metal hose assemblies for aerospace, defense, and other industrial applications.
The company also performs precision cleaning operations requiring strict cleanliness standards [1]. Maintaning consistent processing conditions throughout these operations is essential to producing reliable components that meet customer expectations.

Modern manufacturing processes demand precise control, consistent operating conditions, and reliable monitoring systems to ensure product quality and operational efficiency. These requirements are particularly critical in sectors such as aerospace and defense, where manufacturing defects may result in severe consequences. Flexial Corporation manufactures precision metal bellows, accumulators, and flexible metal hose assemblies for aerospace, defense, and other industrial applications. The company also conducts precision cleaning operations for components that must meet stringent cleanliness standards [1]. Consistent processing conditions throughout these operations are essential for producing reliable components that fulfill customer requirements.

To address challenges in monitoring and controlling manufacturing equipment, the senior design team is developing an automation system for Flexial based on a programmable logic controller (PLC). The proposed system will integrate chemical tank monitoring, temperature regulation, valve operation, and process identification within a centralized control framework. Utilizing industrial sensors, a PLC, and a human-machine interface (HMI), the system will provide operators with real-time access to process conditions and enable automated execution of selected operations. The project will also explore the integration of barcode scanning and manufacturing data collection to enhance traceability throughout the production process. These enhancements are intended to reduce manual intervention, improve process consistency, and increase manufacturing efficiency.

This proposal outlines the background of the manufacturing process and identifies the technical challenges associated with implementing an automated control system. A review of existing industrial automation solutions will evaluate available controllers, sensors, and communication technologies to inform the system design. Subsequently, the proposal will define system specifications and constraints, establish measurable success criteria, and detail the resources necessary for implementation, including equipment costs, personnel, and a project timeline. Finally, the proposal will address the specific benefits for Flexial and broader implications of industrial automation, such as safety considerations and professional engineering responsibilities.

## Formulating the Problem

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

-The system shall measure the temperature of the drying ovens and the time a part is in the ovens.

- The system shall measure and read values similar to the cleaning tanks for the passivation tanks

- The system shall be able to ensure that a part comes out of cleaning properly and will notify the user if any error is found.

- The system may have more steps of the fabrication process added to it, such as heat treating, forming, and welding.

## Constraints

- The system shall be able to have more operations of the fabrication process added to it.

- The system shall use 4-20mA analog sensors to measure and read values from the cleaning tanks.

- The system shall allow for replacement sensors so if they wear out or are damaged the system does not have to be redone.

- The system shall follow all regulations of logic, motor control, code safety, and all other coding regulations detailed in IEC 61131 [4].

- The system shall follow all electrical, component, and cybersecurity safety regulations detailed in IEC 62443 [5]. 

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

## Measures of Success

Team 7 will evaluate the success of the Flexial PLC Programming and Process Controls project based on four main factors: **accuracy, reliability, usability and accessibility, and cost-effectiveness.** These factors will help determine how well the PLC systems perform, how easily operators can use them, and how effectively they can be implemented into Flexial's existing processes. The following sections outline the goals and requirements for each factor, along with the methods that will be used to test the system.

## Accuracy

- The system's ability to correctly perform the required operations for each department.
  - Each PLC shall be programmed using ladder logic to control the assigned process.
  - All inputs and outputs (I/O) shall be identified and tested to ensure they respond correctly.
  - The PLC shall complete the required sequence of operations in the correct order without programming errors.
- The system's ability to communicate with Flexial's existing software.
  - The PLC shall be configured to communicate with Flexnet and Epicor using compatible communication methods.
  - Information sent between the PLC and other systems shall be checked to ensure the correct data is being transferred.
  - Each programmed process shall be tested multiple times to verify consistent operation.

## Reliability

- The system's ability to operate safely and consistently during normal production.
  - The PLC shall be capable of operating for extended periods without unexpected interruptions caused by programming errors.
  - Safety features shall be included to prevent equipment from operating under unsafe conditions.
  - The system shall recognize incorrect operating conditions and stop the process when necessary.
- The system's ability to handle unexpected problems.
  - The PLC shall respond safely to power loss, communication errors, and other possible faults.
  - The system shall provide fault indicators to help operators identify problems.
  - Each process shall successfully complete at least 20 consecutive cycles without a programming-related failure.

## Usability and Accessibility

- The system's ability to be easily operated by Flexial employees.
  - A user interface shall be developed to allow operators to control and monitor the process.
  - The interface shall provide clear instructions to guide operators through each step.
  - The system shall include features that help reduce human errors during operation.
- The system's ability to be maintained and modified when needed.
  - Team 7 shall provide documentation of the PLC programs, hardware requirements, and I/O connections.
  - PLC programs shall be organized to make troubleshooting and future changes easier.
  - The required hardware and software shall be identified so replacement components can be obtained when needed.
- The system's ability to support employee training.
  - A training procedure shall be developed to explain how to operate the system.
  - Operators shall be able to follow the instructions provided through the user interface to complete the process.

## Cost-Effectiveness

- The system's ability to provide an affordable solution for improving Flexial's production processes.
  - Team 7 shall create a list of all hardware and software needed to implement the PLC systems.
  - The total estimated cost of the equipment and implementation shall be documented.
  - Existing equipment shall be used whenever possible to reduce additional expenses.
  - A phased implementation plan shall be created to outline the expected costs and time required for each stage of the project.

## Testing Methodology

### Accuracy

- Each PLC program shall be tested to ensure the ladder logic performs the correct sequence of operations.
- All inputs and outputs shall be individually checked for proper functionality.
- Communication with Flexnet and Epicor shall be tested when the necessary connections are available.

### Reliability

- Each process shall be tested for at least 20 consecutive cycles to confirm consistent performance.
- Safety features and fault detection shall be tested by introducing simulated errors.
- The PLC shall be tested to verify that it responds appropriately to interruptions and unexpected conditions.

### Usability

- The user interface shall be tested to confirm operators can start, stop, and monitor the process.
- The step-by-step training procedure shall be demonstrated to evaluate how easily an operator can follow the instructions.
- Team 7 shall demonstrate how the PLC program can be adjusted or troubleshot when necessary.

### Cost-Effectiveness

- The implementation plan shall be reviewed to determine whether the proposed timeline and expenses are reasonable.
- All required equipment and software costs shall be recorded and compared with the project's available budget.

## Resources

Each project proposal must include a comprehensive description of the necessary resources.

### Budget

# Team 7: Budget Document

Team 7 has a total budget of approximately **$40,000–$50,000**. This budget is intended to provide Flexial with a fully assembled and working PLC system.

Flexial has a three-phase plan to implement the full PLC system. At this time, many costs are unknown because Team 7 has not received the complete plan and/or selected all parts due to outstanding details from Flexial.

## Preliminary Budget

| Item | Price ($) |
| --- | ---: |
| PLC Central Processor | N/A |
| Memory | N/A |
| Power Supply | N/A |
| Tank Temperature Sensors (4) | N/A |
| Oven Temperature Sensor (1) | N/A |
| Total Dissolved Solid Sensors (4) | N/A |
| pH Sensors (4) | N/A |
| Concentration Sensors (4) | N/A |

## Project Timeline and Budget Updates

As stated above, this is a three-phase project. The budget table includes only part of Phase 1 of the overall project. Team 7 is working with the timeline provided by Flexial, so the table is expected to change significantly as the system progresses.

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

<img width="1866" height="736" alt="image" src="https://github.com/user-attachments/assets/38e3a3e8-f966-423d-9ea4-7c4800af35b6" />


## Specific Implications

There are a multitude of reasons for the PLC to be put into place within the company. There are many workers that interact with dangerous chemicals and potential hazards, the automation of the process will provide a safer work environment for employees. The PLC will also have the intention in reducing errors that can be made by people, making sure that everything that leaves it is consistent. A better consistency will also allow for more money to be saved by having less product incorrectly handled, resulting in less waste. The speed of the process should also be faster, having a machine that can process more materials than the average worker can handle with the same quality. 

## Broader Implications, Ethics, and Responsibility as Engineers

A broader implication that can be taken from this machine is the fact that reducing waste also helps lessen pollution being added to the environment. If parts are constantly being thrown away then that creates more of a possibility that it affects the environment. There are potential workers that are spared from injury and it also protects the company from dealing with any kind of legal trouble, within proper use of the machine. It is possible that the automation of these processes may remove some of the available jobs for older workers, but it also opens the possibility of them learning to handle machinery or be moved into an arguably better position. Every project also has to consider what happens if anything within the machine fails, this risk should be mitigated by having failsafes that will remove/ contain anything that could harm a worker. 

## References

All sources used in the project proposal that are not common knowledge must be cited. Multiple references are required.
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

Each team member must contribute meaningfully to the project proposal. In this section, each team member is required to document their individual contributions to the report. One team member may not record another member's contributions on their behalf. By submitting, the team certifies that each member's statement of contributions is accurate.

James: Personal section, Survey of existing solutions section.

George: Specifications, Constraints, Gantt Chart

Phillip: Introduction, Background

Izaiah:Specific & Broader implications
