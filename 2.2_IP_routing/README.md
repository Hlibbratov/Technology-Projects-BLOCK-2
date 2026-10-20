
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

# Part A — Connect the Raspberry Pis

Connect the Ethernet cable directly between the Ethernet ports of Raspberry Pi A and Raspberry Pi B.

On **both Raspberry Pis**, check that the Ethernet interface exists:

```bash
ip link show eth0
```

You should see an interface called `eth0`.

Now check NetworkManager:

```bash
nmcli device status
```

Look for `eth0` in the output.

If Ethernet is not detected or the interface is disconnected, check the Ethernet cable and connectors before continuing.

---

# Part B — Configure Static IP Addresses

We will create the following LAN:

- **Raspberry Pi A:** `192.168.50.1/24`
- **Raspberry Pi B:** `192.168.50.2/24`
- **Network:** `192.168.50.0/24`

No gateway is required because the Raspberry Pis are communicating directly with each other.

## 2.1 Find the Ethernet Connection Name

On each Raspberry Pi, run:

```bash
nmcli connection show
```

Find the connection associated with Ethernet. It may be called:

```text
Wired connection 1
```

> If your connection has a different name, use that name in the commands below.

---

## 2.2 Configure Raspberry Pi A

Run:

```bash
sudo nmcli connection modify "Wired connection 1" \
    ipv4.method manual \
    ipv4.addresses 192.168.50.1/24 \
    ipv4.gateway "" \
    ipv4.dns ""
```

Restart the connection:

```bash
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

---

## 2.3 Configure Raspberry Pi B

Run:

```bash
sudo nmcli connection modify "Wired connection 1" \
    ipv4.method manual \
    ipv4.addresses 192.168.50.2/24 \
    ipv4.gateway "" \
    ipv4.dns ""
```

Restart the connection:

```bash
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

---

# Part C — Verify the Network Configuration

Before using `ping`, check that each Raspberry Pi has the correct IP address.

## Raspberry Pi A

```bash
ip addr show eth0
```

Look for:

```text
inet 192.168.50.1/24
```

## Raspberry Pi B

```bash
ip addr show eth0
```

Look for:

```text
inet 192.168.50.2/24
```

On either Raspberry Pi, examine the routing table:

```bash
ip route
```

You should see a route for the local network similar to:

```text
192.168.50.0/24 dev eth0
```

---

# Part D — Test Connectivity

## From Raspberry Pi A

```bash
ping -c 4 192.168.50.2
```

## From Raspberry Pi B

```bash
ping -c 4 192.168.50.1
```

A successful reply will look similar to:

```text
64 bytes from 192.168.50.2: icmp_seq=1 ttl=64 time=0.4 ms
```

The exact response time may be different.

If `ping` does not work, check the following before continuing:

1. Is `eth0` visible with `ip link show eth0`?
2. Does `nmcli device status` show the Ethernet interface?
3. Does Pi A have `192.168.50.1/24`?
4. Does Pi B have `192.168.50.2/24`?
5. Is the Ethernet cable connected correctly?

Do not continue to SSH or the Python program until `ping` works.

---

# Part E — Enable and Test SSH

SCP and SSHFS use SSH, so SSH should be tested first.

## 5.1 Enable SSH on Raspberry Pi B

On Pi B, run:

```bash
sudo raspi-config
```

Navigate to:

```text
Interface Options → SSH → Enable
```

Alternatively:

```bash
sudo systemctl enable --now ssh
```

Check the SSH service:

```bash
systemctl status ssh
```

Press `q` to exit the status screen.

---

## 5.2 Find the Username on Pi B

On Pi B:

```bash
whoami
```

Remember the username shown by the command.

In the following examples, replace `USERNAME` with this username.

---

## 5.3 Connect from Pi A to Pi B

On Pi A:

```bash
ssh USERNAME@192.168.50.2
```

For example, if the username on Pi B is `student`:

```bash
ssh student@192.168.50.2
```

The first time you connect, SSH may ask whether you trust the host. Read the message and follow the prompt.

Once connected, you are controlling Pi B remotely from Pi A.

Check:

```bash
hostname
```

Then return to Pi A:

```bash
exit
```

---

# Part F — Transfer a File with SCP

On Raspberry Pi A, create a test file:

```bash
echo "Hello from Raspberry Pi A" > testfile.txt
```

Check it:

```bash
cat testfile.txt
```

Transfer it to Pi B:

```bash
scp testfile.txt USERNAME@192.168.50.2:~/
```

On Raspberry Pi B, verify the contents:

```bash
cat ~/testfile.txt
```

You should see:

```text
Hello from Raspberry Pi A
```

---

# Part G — Shared Folder with SSHFS

SSHFS allows a directory located on another computer to appear as if it were a local directory.

## 7.1 Create the Shared Folder on Pi B

On Pi B:

```bash
mkdir -p ~/shared
echo "File stored on Pi B" > ~/shared/hello.txt
```

Check:

```bash
ls ~/shared
```

---

## 7.2 Install SSHFS on Pi A

On Pi A:

```bash
sudo apt update
sudo apt install sshfs
```

Create a mount point:

```bash
mkdir -p ~/shared_pi_b
```

Mount Pi B's shared directory:

```bash
sshfs USERNAME@192.168.50.2:/home/USERNAME/shared ~/shared_pi_b
```

Replace both occurrences of `USERNAME` with the actual username on Pi B.

For example:

```bash
sshfs student@192.168.50.2:/home/student/shared ~/shared_pi_b
```

Now test the mounted folder:

```bash
ls ~/shared_pi_b
cat ~/shared_pi_b/hello.txt
```

You should see:

```text
File stored on Pi B
```

When finished, unmount it:

```bash
fusermount3 -u ~/shared_pi_b
```

---

# Part H — Python LAN Chat Program

We will now create our own TCP application.

- Pi A will act as the **server**.
- Pi B will act as the **client**.
- TCP port `5000` will be used.

The network must already be working before attempting this section.

---

## 8.1 Server — Raspberry Pi A

Create the program:

```bash
nano server.py
```

Enter:

```python
import socket

HOST = "192.168.50.1"
PORT = 5000

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server:
    server.bind((HOST, PORT))
    server.listen(1)

    print(f"Waiting for Pi B on {HOST}:{PORT}...")

    conn, addr = server.accept()

    with conn:
        print("Connected by:", addr)

        while True:
            message = conn.recv(1024)

            if not message:
                break

            print("Pi B:", message.decode())

            reply = input("Pi A: ")
            conn.sendall(reply.encode())
```

Save the file and run:

```bash
python3 server.py
```

You should see:

```text
Waiting for Pi B on 192.168.50.1:5000...
```

This is normal. The server is waiting for the client to connect.

---

## 8.2 Client — Raspberry Pi B

Create the program:

```bash
nano client.py
```

Enter:

```python
import socket

HOST = "192.168.50.1"
PORT = 5000

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as client:
    client.connect((HOST, PORT))

    print("Connected to Pi A")

    while True:
        message = input("Pi B: ")
        client.sendall(message.encode())

        reply = client.recv(1024)

        if not reply:
            break

        print("Pi A:", reply.decode())
```

Run:

```bash
python3 client.py
```

Pi B should report:

```text
Connected to Pi A
```

Pi A should report that a client has connected.

You can now exchange messages between the two Raspberry Pis.

---

# Troubleshooting Sequence

When something does not work, troubleshoot in this order:

```text
1. Ethernet interface
       ↓
   ip link show eth0

2. Ethernet connection
       ↓
   nmcli device status

3. IP configuration
       ↓
   ip addr show eth0

4. IP connectivity
       ↓
   ping

5. Remote access
       ↓
   ssh

6. File transfer
       ↓
   scp / sshfs

7. Application layer
       ↓
   Python sockets
```

Do not jump directly to the Python program. Each stage depends on the previous stages working correctly.

