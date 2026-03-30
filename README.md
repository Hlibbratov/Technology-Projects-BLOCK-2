# Technology Projects - Block 2

A comprehensive collection of hands-on networking and IoT projects designed for students to develop practical skills in network configuration, IP routing, subnetting, and IoT services using Raspberry Pi devices.

---

## 📚 Project Structure

This repository is organized into three main technology blocks:

### 1. **2.1_networks** — Network Fundamentals
Introduction to network concepts and hands-on Raspberry Pi networking.

- **network1**: Basic network setup and configuration
  - Summary and objectives
  - Topology design
  - IP configuration
  - Connectivity testing
  - Reflection and analysis

- **network2**: Advanced network scenarios
  - Objectives and planning
  - Network topology and setup
  - Server configuration
  - Client setup
  - Testing procedures
  - Reflection on implementation

### 2. **2.2_IP_routing** — Building a LAN with Raspberry Pis
A practical activity where students build and test a Local Area Network (LAN) between two Raspberry Pis.

**Key Topics:**
- Crimping Ethernet cables (T568B standard)
- Configuring static IP addresses
- Testing connectivity with `ping`
- Practical LAN applications:
  - File transfer using SCP
  - Shared folders via SSHFS
  - Python socket-based chat program

**Prerequisites:**
- 2 × Raspberry Pi with Ethernet ports
- RJ45 connectors and crimping tool
- CAT5e/CAT6 Ethernet cable
- Basic command-line knowledge

### 3. **2.3_subnetting** — IoT Services and Applications
Hands-on exercises in IoT concepts and services using Raspberry Pi.

**Topics:**
- Reading and monitoring Raspberry Pi temperature
- Cloud service integration
- Python publish-subscribe (pub/sub) messaging
- IoT service architecture and deployment

---

## 🎯 Learning Objectives

By completing the projects in this repository, students will be able to:

- ✅ Understand network topology and design principles
- ✅ Configure static IP addresses on Linux systems
- ✅ Troubleshoot network connectivity issues
- ✅ Crimp and test Ethernet cables
- ✅ Build practical networked applications in Python
- ✅ Design and implement IoT services
- ✅ Integrate cloud services with embedded devices
- ✅ Work with pub/sub messaging patterns

---

## 📋 How to Use This Repository

1. **Start with Block 2.1** to understand network fundamentals
2. **Progress to Block 2.2** for hands-on LAN setup and practical applications
3. **Finish with Block 2.3** to explore IoT services and cloud integration

Each section includes:
- Detailed step-by-step guides
- Code examples and templates
- Reflection exercises
- Testing procedures

---

## 🛠️ Requirements

### Hardware
- 2 × Raspberry Pi (with Ethernet recommended)
- Power supplies
- microSD cards with Raspberry Pi OS
- RJ45 connectors
- Ethernet cables
- Crimping tool

### Software
- Raspberry Pi OS (Linux-based)
- Python 3.x
- SSH client (for remote access)
- Basic terminal/command-line tools

---

## 📖 Getting Started

1. Clone or download this repository
2. Read the relevant section's README and documentation
3. Gather required materials
4. Follow the step-by-step instructions in each module
5. Complete the practical activities
6. Document your results and reflections

---

## 📝 Documentation Structure

Each subsection follows a consistent structure:

- **01_summary/objective** — Goals and overview
- **02_topology/setup** — Network design and configuration
- **03_configuration/server** — IP and service setup
- **04_connectivity/clients** — Testing and client setup
- **05_reflection/testing** — Analysis and evaluation
- **README.md** — Module-specific instructions

---

## 💡 Tips for Success

- Carefully follow the wiring standards (T568B) when crimping cables
- Test connectivity at each step before proceeding
- Document your configuration in case troubleshooting is needed
- Use `ifconfig` and `ip addr` to verify IP configuration
- Keep detailed notes in the reflection sections
- Test applications thoroughly before declaring them complete

---

## 🔧 Troubleshooting

### Network Not Connecting
- Verify the Ethernet cable is properly crimped and connected
- Check that both Raspberry Pis have static IPs configured
- Use `ping` to test basic connectivity
- Review the IP configuration files

### Python Applications Not Running
- Ensure Python 3 is installed: `python3 --version`
- Install required libraries as specified in the activity
- Check that IP addresses match the configuration

### SSH Connection Issues
- Ensure both Pis are on the same network segment
- Verify SSH is enabled on the target Raspberry Pi
- Check firewall settings if applicable


