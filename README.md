

# Robotic Arm Project

Welcome to the Robotic Arm Project! This repository contains the code and instructions to install and run the robotic arm. Follow the steps below to get started.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Robotic Arm](#running-the-robotic-arm)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

Before you begin, ensure you have the following prerequisites installed:

- Python 3.8 or later
- Pip (Python package manager)
- [Xarm Studio](https://www.ufactory.cc/ufactory-studio/)
- [xArm Python SDK](https://github.com/xArm-Developer/xArm-Python-SDK)

## Installation

Follow these steps to clone the repository and install the necessary dependencies:

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/ufactory-xarm7.git
    cd ufactory-xarm7
    ```

2. Create and activate a virtual environment (recommended):
    ```bash
    python -m venv venv
    source venv/bin/activate   # On Windows, use `venv\Scripts\activate`
    ```

3. Install the required dependencies:
    ```bash
    pip install -r requirements.txt
    ```

4. Install the xArm Python SDK:
    ```bash
    pip install git+https://github.com/xArm-Developer/xArm-Python-SDK.git
    ```

## Configuration

Before running the UFactory xArm7, you need to configure the settings:

1. Create a configuration file by copying the example file:
    ```bash
    cp config.example.json config.json
    ```

2. Edit `config.json` to match your setup. Make sure to specify the correct serial port or IP address and other necessary parameters. Example `config.json`:
    ```json
    {
      "port": "/dev/ttyUSB0",  # For USB connection
      "ip": "192.168.1.1",     # For Ethernet connection
      "baudrate": 115200,
      "timeout": 10
    }
    ```

## Running the UFactory xArm7

Once the installation and configuration are complete, you can run the UFactory xArm7 using the following command:

```bash
python main.py
```

Here is a basic example of a main.py script to control the xArm7:
```python
import json
from xarm.wrapper import XArmAPI

# Load configuration
with open('config.json') as config_file:
    config = json.load(config_file)

# Connect to xArm
arm = XArmAPI(config['ip'], baud_checkset=False)

# Initialize the arm
arm.motion_enable(enable=True)
arm.set_mode(0)
arm.set_state(0)

# Example: Move to a position
arm.set_position(x=200, y=0, z=150, speed=50, wait=True)

# Disconnect
arm.disconnect()
```

