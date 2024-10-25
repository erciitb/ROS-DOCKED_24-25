# Docker and ROS Setup Guide

This repository contains the files required to install Docker and ROS. Go through the README file, please.

## Visual Studio Code

### Installation
- [Download VS Code](https://code.visualstudio.com/download)

### Setup

#### Windows
- [Setup Instructions for Windows](https://code.visualstudio.com/docs/setup/windows)

#### Linux
- [Setup Instructions for Linux](https://code.visualstudio.com/docs/setup/linux)

#### macOS
- [Setup Instructions for macOS](https://code.visualstudio.com/docs/setup/mac)

### Video Reference
- [VS Code Setup Video](https://youtu.be/bN6DE-4uFNo?feature=shared)

## Ubuntu and Docker Setup on Windows

### Basic Setup
1. Search for "Turn Windows features on and off".
2. Enable "Hyper-V" and "Windows Subsystem for Linux".

![Screenshot 2024-07-27 110932](https://github.com/user-attachments/assets/14a63d46-4be2-4e31-8dd7-a51f2c569afa)
![Screenshot 2024-07-27 113538](https://github.com/user-attachments/assets/df1e554d-ccc8-4cee-94f1-016ea8505b5d)


---

## Docker

### System Requirements and Installation

#### macOS
- [Docker Installation for macOS](https://docs.docker.com/desktop/install/mac-install/)

#### Windows
- [Docker Installation for Windows](https://docs.docker.com/desktop/install/windows-install/)

#### Linux
- [Docker Installation for Linux](https://docs.docker.com/desktop/install/linux-install/)

### Starting Docker Desktop
- Start Docker Desktop and ensure it is running.

### Video Tutorial
- [Docker Setup Video (up to 5:48)](https://youtu.be/dihfA7Ol6Mw?feature=shared) (Note: Download Humble Desktop Full)
---

## Ubuntu

### Installation and Setup
- Download Version: Ubuntu 22.04 LTS from microsoft store 
- [Ubuntu on WSL2 Installation Guide](https://linuxsimply.com/linux-basics/os-installation/wsl/ubuntu-on-wsl2/)

## Step 1: Setting Up Ubuntu

1. **Open the Ubuntu Terminal**:
   - Search for "Ubuntu" in the Windows Start menu and open it.

2. **Fill in the UNIX Name and Password**:
   - During the first run, you'll be asked to create a UNIX username and password. Make sure to **remember these details** as they will be needed for future administrative tasks.

## Step 2: Allowing Ubuntu to Run Docker

1. **Start Docker Desktop**:
   - Open **Docker Desktop** from the Windows Start menu.

2. **Navigate to Settings**:
   - In Docker Desktop, click the **Settings** button.

3. **Enable WSL 2 Engine**:
   - Under the **General** tab, select the option **Use WSL 2 based engine**.
   - If your system supports WSL 2, this option will be turned on by default.

4. **Apply & Restart**:
   - Click the **Apply & Restart** button to apply the changes.

---

## Step 3: Set Ubuntu 22.04 as the Default WSL Version

1. Open **Command Prompt** or **PowerShell** on your Windows machine.

2. Run the following command to set Ubuntu 22.04 as the default WSL version:
   ```bash
   wsl.exe --set-default Ubuntu 22.04


## Using VS Code with Docker

1. Open VS Code in the desired folder.

2. Go to the Extensions view by clicking the Extensions icon in the Activity Bar on the side of the window.

3. Search for "Dev Containers" and install the "Remote Development" extension pack.

![image](https://github.com/user-attachments/assets/bf316684-5100-473a-977a-738bc4bcdefe)
![image](https://github.com/user-attachments/assets/10f3373f-d1b5-4a2c-acb5-f7787fb88638)

4. Click on the bottom-left corner (left to the launch pad).

![Screenshot 2024-07-27 115457](https://github.com/user-attachments/assets/cea1a97a-283c-4ebb-b4d3-0a3125f53d81)

5. Select "Reopen in Container".

![image](https://github.com/user-attachments/assets/dd38d66c-65c0-4c04-a8e4-78d41a8bb3b8)

6. Add configuration to the data folder.

7. Search for "ROS" and select "Humble".

![image](https://github.com/user-attachments/assets/1544ffef-33b6-413f-b795-07291b427317)

8. Select "Desktop Full".

![image](https://github.com/user-attachments/assets/9ce6985e-72fb-4ff9-9d0c-d115795d2728)
![image](https://github.com/user-attachments/assets/ed7577b7-3c2e-43db-b34e-e5cbfa6b0cb5)

# Moving Robot Simulation Instructions

Follow the steps below to set up and run the moving robot simulation using Ignition Gazebo.

## Prerequisites
- Ensure you have Ignition Gazebo installed and properly configured.
- Open Visual Studio Code (VS Code) with the necessary extensions for Docker.

## Steps

1. **Download the Simulation File**
   - Download the robot simulation file from the following link:
     ```bash
      https://github.com/prerak142/DOCKER-101-/blob/main/moving_robot.sdf
     ```
   - Save the downloaded file in the folder that you opened in VS Code.

2. **Open the Terminal in VS Code**
   - Open the integrated terminal in VS Code. You should see a prompt similar to `user@docker-host`.
   - ![image](https://github.com/user-attachments/assets/9863d0a8-30f1-4d47-a2c2-bc8c1e650cac)

3. **Run the Simulation**
   - Execute the following command to start the simulation:
     ```bash
     ign gazebo moving_robot.sdf
     ```

4. **Access the Gazebo Interface**
   - The Gazebo interface will appear. It should look similar to the image below:
   ![Gazebo Interface](https://github.com/user-attachments/assets/b452c727-f67d-4718-80c3-1a6b83163e08)

5. **Configure the Robot Control**
   - Click on the three dots appearing at the top of the interface and search for **Key Publisher**.

6. **Open a New Terminal**
   - In the new terminal, run the following command to publish velocity commands:
     ```bash
     ign topic -t "/cmd_vel" -m ignition.msgs.Twist -p "linear: {x: 0.5}, angular: {z: 0.05}"
     ```

7. **Start the Robot Movement**
   - Your robot should now start moving in the simulation. Make sure to press the **Play** button in the Gazebo interface to begin the simulation.

8. **Control the Robot via Keyboard**
   - To control the robot using keyboard inputs, run the following command in the terminal:
     ```bash
     ign topic -e -t /keyboard/keypress
     ```
   - The following keyboard mappings are available for controlling the robot:
     - **Left** ➞ `16777234` ➞ `linear: {x: 0.0}, angular: {z: 0.5}`
     - **Up** ➞ `16777235` ➞ `linear: {x: 0.5}, angular: {z: 0.0}`
     - **Right** ➞ `16777236` ➞ `linear: {x: 0.0}, angular: {z: -0.5}`
     - **Down** ➞ `16777237` ➞ `linear: {x: -0.5}, angular: {z: 0.0}`

## Note
Ensure that the simulation is running smoothly by monitoring the Gazebo interface for any errors.

**Happy Learning!**
