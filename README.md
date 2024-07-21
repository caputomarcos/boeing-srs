# BOEING ![image](https://github.com/user-attachments/assets/2ba0e2b4-1a6f-49f8-a6c5-f3607651d041) - Software Requirements Specification (SRS) 


## 1. Introduction

### 1.1 Purpose
This Software Requirements Specification (SRS) document provides a comprehensive overview of the PLC control system developed using Node-RED. This document aims to define the system’s functionalities, requirements, constraints, and interactions to ensure a clear understanding among all stakeholders.

### 1.2 Scope
The PLC control system is designed to facilitate industrial automation by enabling operators to send commands to a Programmable Logic Controller (PLC). The system primarily focuses on buzzer control and crane operations. This SRS outlines the essential requirements for developing, testing, and maintaining the system.

### 1.3 Definitions, Acronyms, and Abbreviations
- **PLC**: Programmable Logic Controller
- **Node-RED**: Flow-based development tool for visual programming
- **SRS**: Software Requirements Specification

### 1.4 References
- Node-RED Documentation: [Node-RED Documentation](https://nodered.org/docs/)
- Modbus Protocol Standards: [Modbus Protocol](https://modbus.org/)

### 1.5 Overview
This document details the functional and non-functional requirements, system architecture, user interface, and maintenance aspects of the PLC control system.

## 2. Overall Description

### 2.1 Product Perspective
The PLC control system integrates into the broader industrial automation ecosystem. It enables human operators to interact with automated processes through a user-friendly interface, ensuring efficient management and control of critical operations.

### 2.2 Product Features
- **Buzzer Control**: Commands to activate and deactivate the buzzer.
- **Crane Operations**: Commands to stop and release the crane.
- **User Interface**: Intuitive dashboard for operators.
- **Logging and Debugging**: Detailed logs for monitoring and troubleshooting.

### 2.3 User Classes and Characteristics
- **Production Operators**: Require an easy-to-use interface to control PLC operations.
- **Control Engineers**: Need access to detailed logs and system status for maintenance and troubleshooting.

### 2.4 Constraints
- The system must be developed using Node-RED.
- Communication with the PLC must use the Modbus TCP protocol.
- The system must ensure high availability and security.

### 2.5 Assumptions and Dependencies
- Reliable network communication between Node-RED and the PLC.
- Users have basic training in operating the system.

## 3. Specific Requirements

### 3.1 Functional Requirements

#### 3.1.1 Buzzer Control
- **Description**: The system must allow operators to clear the buzzer by sending a command to the PLC.
- **Acceptance Criteria**: The buzzer should be deactivated within 3 seconds of sending the command.

```mermaid
flowchart TD
    Operator --> UserInterface
    UserInterface --> NodeRED
    NodeRED --> PLC
    PLC --> Buzzer
```

#### 3.1.2 Crane Stop
- **Description**: The system must allow operators to stop the crane by sending a command to the PLC.
- **Acceptance Criteria**: The crane should stop within 3 seconds of sending the command.

```mermaid
flowchart TD
    Operator --> UserInterface
    UserInterface --> NodeRED
    NodeRED --> PLC
    PLC --> Crane
```

#### 3.1.3 Crane Release
- **Description**: The system must allow operators to release the crane by sending a command to the PLC.
- **Acceptance Criteria**: The crane should be released within 3 seconds of sending the command.

```mermaid
flowchart TD
    Operator --> UserInterface
    UserInterface --> NodeRED
    NodeRED --> PLC
    PLC --> Crane
```

### 3.2 Non-Functional Requirements

#### 3.2.1 Performance
- **Description**: The system must process and send commands to the PLC within 1 second.
- **Acceptance Criteria**: Average command processing time should be below 1 second.

#### 3.2.2 Reliability
- **Description**: The system must maintain 99.9% uptime.
- **Acceptance Criteria**: System availability should be at least 99.9%.

#### 3.2.3 Usability
- **Description**: The interface must be intuitive for production operators.
- **Acceptance Criteria**: Operators should be able to perform tasks with minimal training.

#### 3.2.4 Security
- **Description**: Only authorized users should be able to send critical commands.
- **Acceptance Criteria**: Authentication and access control must be implemented.

## 4. System Models and Diagrams

### 4.1 Flow Diagrams

#### 4.1.1 General Flow Diagram

```mermaid
flowchart TD
    Operator --> UserInterface
    UserInterface --> CommandNodes
    CommandNodes --> DelayNodes
    DelayNodes --> DebugNodes
    DebugNodes --> PLC
    PLC --> Devices
```

### 4.2 Sequence Diagrams

#### 4.2.1 Command Sequence

```mermaid
sequenceDiagram
    participant Operator
    participant UserInterface
    participant NodeRED
    participant PLC

    Operator ->> UserInterface: Send Command
    UserInterface ->> NodeRED: Forward Command
    NodeRED ->> PLC: Send Command
    PLC ->> NodeRED: Acknowledge Command
    NodeRED ->> UserInterface: Update Status
    UserInterface ->> Operator: Display Status
```

### 4.3 Class Diagrams

#### 4.3.1 System Classes

```mermaid
classDiagram
    class UserInterface {
        +sendCommand(command)
        +updateStatus(status)
    }

    class CommandNode {
        +processCommand(command)
        +sendToPLC(command)
    }

    class DelayNode {
        +addDelay(duration)
    }

    class DebugNode {
        +logStatus(status)
    }

    class PLC {
        +receiveCommand(command)
        +sendStatus()
    }

    UserInterface -- CommandNode
    CommandNode -- DelayNode
    DelayNode -- DebugNode
    DebugNode -- PLC
```

### 4.4 Entity Relationship Diagram

#### 4.4.1 System Entities

```mermaid
erDiagram
    USER {
        int user_id
        string name
        string role
    }

    COMMAND {
        int command_id
        string type
        string status
    }

    LOG {
        int log_id
        string message
        datetime timestamp
    }

    USER ||--o{ COMMAND: sends
    COMMAND ||--o{ LOG: generates
```

## 5. User Interface

### 5.1 Overview
The user interface is designed to be intuitive and user-friendly, allowing operators to send commands and monitor system status with ease. It consists of the following components:

- **Dashboard**: Displays real-time status of the PLC and connected devices.
- **Command Panel**: Allows operators to send commands to the PLC.
- **Log Panel**: Shows detailed logs for debugging and monitoring.

### 5.2 User Journey

```mermaid
journey
    title User Journey for PLC Control System
    section Sending a Command
      Operator: 5: Open the User Interface
      Operator: 5: Select Command to Send
      Operator: 5: Confirm and Send Command
    section Monitoring Status
      Operator: 4: View Real-Time Status on Dashboard
      Operator: 4: Check Logs for Command Acknowledgment
    section Troubleshooting
      Engineer: 4: Access Log Panel
      Engineer: 3: Analyze Logs for Errors
      Engineer: 4: Perform Necessary Troubleshooting
```

## 6. HTML Integration

### 6.1 Overview
The user interface is built using HTML, CSS, and JavaScript to provide a responsive and interactive experience. The HTML components are designed to integrate seamlessly with Node-RED, enabling real-time updates and command execution.

### 6.2 Components
- **Dashboard**: Displays real-time data and status indicators.
- **Command Panel**: Provides buttons and input fields for sending commands.
- **Log Panel**: Displays logs and system messages for monitoring and debugging.

## 7. Maintenance and Support

### 7.1 Logging and Monitoring
The system includes comprehensive logging and monitoring capabilities to track command execution and system status. Logs are accessible through the user interface and can be exported for further analysis.

### 7.2 Updates and Upgrades
Regular updates and upgrades will be provided to ensure the system remains secure and up-to-date with the latest features and improvements.

### 7.3 Technical Support
Technical support is available to assist with any issues or questions related to the system. Support includes troubleshooting, bug fixes, and guidance on system usage.

## 8. Appendices

### 8.1 Glossary
- **PLC**: Programmable Logic Controller
- **Node-RED**: Flow-based development tool for visual programming
- **Modbus**: Communication protocol used with PLCs

### 8.2 References
- Node-RED Documentation: [Node-RED Documentation](https://nodered.org/docs/)
- Modbus Protocol Standards: [Modbus Protocol](https://modbus.org/)

This concludes the Software Requirements Specification for the PLC control system.


![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/7880a4ad-89dd-47b1-97fd-31d41c7c3568)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/6bf067a5-9a9c-4348-b25f-90ed4881fd76)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/19e8bbfd-fa9b-45b2-8518-f17b90cd08c2)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/36ee72ca-2e59-4101-bf99-f7cc9dd924e4)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/8b119894-ab5c-4c9f-a9b1-82666adc586f)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/35ff1ceb-0cfe-4f10-b010-5e1f6cf17194)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/2a3e6e40-bc67-4849-ab90-ecb8d576dbe8)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/0b186714-c401-40cb-ade6-a45b34c44128)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/4f596fd6-fc62-4fb6-a6c4-b47754bcd608)
![image](https://github.com/caputomarcos/boeing_flow/assets/3945941/d4323c59-ae23-49b9-993a-a39a8f317252)





