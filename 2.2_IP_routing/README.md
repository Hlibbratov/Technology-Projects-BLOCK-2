
# Practical Activity: Build a Simple LAN Between Two Raspberry Pis

## Overview
In this activity, students will:
1. Crimp their own Ethernet cable.
2. Connect two Raspberry Pis directly to form a LAN.
3. Configure static IP addresses.
4. Test connectivity using `ping`.
5. Use the LAN for a practical application (file transfer, shared folder, or Python chat program).

---

## 1. Materials Required
- 2 × Raspberry Pi with Ethernet
- 2 × microSD cards with Raspberry Pi OS
- Power supplies
- RJ45 connectors
- CAT5e/CAT6 Ethernet cable
- Crimping tool
- Cable tester (optional)
- HDMI display or SSH access

---

## 2. Part A — Crimping Your Own Ethernet Cable

### 2.1 Prepare the Cable
1. Cut a 1–3 m length of Ethernet cable.
2. Strip ~2 cm of the outer jacket.
3. Untwist the wire pairs.

### 2.2 Arrange the Wires (T568B Standard)
Arrange wires **left to right**:
1. White–Orange
2. Orange
3. White–Green
4. Blue
5. White–Blue
6. Green
7. White–Brown
8. Brown

### 2.3 Insert and Crimp
1. Flatten wires and trim evenly.
2. Insert them into the RJ45 connector fully.
3. Crimp using the crimping tool.

### 2.4 Test the Cable
Use a cable tester (recommended). Without one, successful communication later will confirm the wiring.

---

## 3. Part B — Setting Up the LAN
Connect your newly-made cable between the two Raspberry Pis.

### 3.1 Configure Static IPs

#### On Raspberry Pi A:
```bash
sudo nano /etc/dhcpcd.conf
```
Add:
```bash
interface eth0
static ip_address=192.168.50.1/24
```

#### On Raspberry Pi B:
```bash
sudo nano /etc/dhcpcd.conf
```
Add:
```bash
interface eth0
static ip_address=192.168.50.2/24
```

Restart networking:
```bash
sudo systemctl restart dhcpcd
```

---

## 4. Part C — Test Connectivity

### From Raspberry Pi A:
```bash
ping 192.168.50.2
```

### From Raspberry Pi B:
```bash
ping 192.168.50.1
```
Expected output:
```
64 bytes from 192.168.50.2: icmp_seq=1 ttl=64 time=0.4 ms
```
If not, check wiring and static IP config.

---

## 5. Part D — Practical Uses of the LAN

---

### File Transfer with SCP

#### From Raspberry Pi A:
```bash
scp testfile.txt pi@192.168.50.2:/home/pi/
```
Verify on Pi B:
```bash
ls /home/pi/
```

---

### Shared Folder via SSHFS
Install SSHFS on Pi A:
```bash
sudo apt install sshfs
```
Mount Pi B's folder:
```bash
mkdir ~/shared_pi_b
sshfs pi@192.168.50.2:/home/pi/shared ~/shared_pi_b
```
Now Pi A accesses Pi B’s folder like a local directory.

---

### Python LAN Chat Program

#### On Raspberry Pi A (server):
```python
import socket

s = socket.socket()
s.bind(("192.168.50.1", 5000))
s.listen(1)
conn, addr = s.accept()

while True:
    msg = conn.recv(1024).decode()
    print("Pi B:", msg)
    conn.send(input("You: ").encode())
```
Run:
```bash
python3 server.py
```

#### On Raspberry Pi B (client):
```python
import socket

s = socket.socket()
s.connect(("192.168.50.1", 5000))

while True:
    s.send(input("You: ").encode())
    msg = s.recv(1024).decode()
    print("Pi A:", msg)
```
Run:
```bash
python3 client.py
```

---

## 6. Reflection Questions
1. What happens if both Pis have the same IP address?
2. Why are static IPs used in this activity?
3. How does the physical cable differ from logical addressing?
4. How would you expand this LAN with a switch?
5. Why is a crossover cable unnecessary on modern devices?


