# OpenReflector

**OpenReflector** is a command-line tool that deploys and configures the **Anthropic Computer Use container** to control and monitor the desktop environment of the machine where OpenReflector is running (the workstation). By leveraging **OpenAdapt** and **WebSockets**, OpenReflector enables the Anthropic container to interact with the workstation’s desktop as if it were local, allowing the container to be deployed on any machine (e.g., EC2, or the workstation itself) while capturing and controlling actions on the workstation.

## Overview

OpenReflector acts as a bridge between the Anthropic container and OpenAdapt on the workstation, setting up a real-time, two-way connection that streams actions and commands. With OpenReflector, you can:
- **Capture** desktop actions, screenshots, and accessibility data on the workstation using OpenAdapt.
- **Stream** this data to the Anthropic container, allowing it to monitor and interact with the workstation desktop in real-time.
- **Execute** commands from the container back on the workstation, creating a mirrored interaction loop.

This setup allows the Anthropic tools to control and observe the workstation desktop, regardless of the Anthropic container’s location.

## Key Features

- **Flexible Deployment**: OpenReflector can deploy the Anthropic container on local or remote environments (e.g., EC2), allowing it to interact with the workstation’s desktop from anywhere.
- **Real-Time Desktop Mirroring**: Streams desktop interactions and commands between the workstation and the container using WebSocket.
- **Easy-to-Use CLI**: Simple commands to deploy, configure, and manage the interaction between the Anthropic container and OpenAdapt on the workstation.

## Project Components

OpenReflector consists of the following main components:

### CLI Tool (`openreflector`)

The core of OpenReflector is its command-line interface, which:
- **Deploys the Anthropic container** on a specified target (local or remote).
- **Configures WebSocket communication** between the container and the workstation’s OpenAdapt instance.
- **Manages OpenAdapt** on the workstation to handle data capture and playback.

### Container Configuration

OpenReflector uses a Docker configuration for the Anthropic container, adding the necessary environment variables and dependencies to support real-time connection and interaction with the workstation. The setup includes:
- **WebSocket client** in the container to receive data from and send commands to the workstation.
- **Environment Variables** for display, screen size, and WebSocket configuration to direct the container’s tools to the workstation.

### Host Application (OpenAdapt Integration)

OpenAdapt on the workstation captures and executes desktop actions:
- **Data Capture**: OpenAdapt’s recording functionality streams desktop actions, screenshots, and accessibility (A11y) data to the container.
- **Command Execution**: Commands from the container are sent to OpenAdapt’s playback, which performs the specified actions on the workstation.

## Installation

### Prerequisites

- **Docker**: Ensure Docker is installed on the machine where you intend to deploy the Anthropic container.
- **Python**: Install Python and required dependencies for OpenAdapt on the workstation.
- **WebSocket Support**: Ensure network permissions allow WebSocket communication between the container and workstation.

### Install OpenReflector

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/your-username/OpenReflector
    cd OpenReflector
    ```

2. **Install Requirements**:
    ```bash
    pip install -r requirements.txt
    ```

3. **Install OpenAdapt on the Workstation**:
    ```bash
    pip install openadapt
    ```

## Usage

### Deploying the Anthropic Container

You can deploy the Anthropic container on the local machine or a remote server (e.g., EC2).

1. **Deploy Locally**
    ```bash
    openreflector deploy --local
    ```

2. **Deploy Remotely (e.g., EC2)**
    ```bash
    openreflector deploy --ec2 --instance-id <instance-id>
    ```

### Running OpenReflector

Once the container is deployed, you can start OpenReflector to establish the connection and enable real-time desktop mirroring.

1. **Start WebSocket Connection and Run OpenAdapt**
    ```bash
    openreflector run --target <local|ec2>
    ```

OpenReflector will set up a WebSocket connection between the Anthropic container and OpenAdapt on the workstation, allowing the Anthropic tools to control and monitor the workstation desktop.

## Configuration Options

OpenReflector provides configuration options to adjust screen settings, WebSocket ports, and capture rates:

- **Display Variables**: Configure screen size (`WIDTH` and `HEIGHT`) and display number (`DISPLAY_NUM`) for the workstation desktop.
- **WebSocket Server**: Update IP address and port to customize WebSocket communication.
- **Capture Rate**: Adjust intervals and image resolution to optimize performance based on network and hardware capabilities.

## Example Commands

### Deploy the Container on Local Docker

```bash
openreflector deploy --local
```

### Deploy on EC2 with Workstation Mirroring

```bash
openreflector deploy --ec2 --instance-id <instance-id>
```

### Run OpenReflector to Mirror Workstation Desktop

```bash
openreflector run --target <local|ec2>
```

## Troubleshooting

- **Connection Issues**: Check network and firewall settings to ensure WebSocket communication is enabled between the workstation and the container. Verify Docker’s network configuration if running locally.
- **Performance Optimization**: Reduce capture rates or resolution if latency is high. OpenAdapt handles cross-platform input injection, so configuration on the workstation may improve responsiveness.

## Future Directions

- **Security Enhancements**: Optional access controls for shared workstations.
- **Expanded Platform Support**: Further optimizations for Windows and Mac environments.
- **Additional Integrations**: Compatibility with other automation tools for more flexible usage scenarios.

## License

This project is licensed under the MIT License.
