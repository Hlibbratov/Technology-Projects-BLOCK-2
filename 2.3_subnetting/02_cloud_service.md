
# Creating a HiveMQ Cloud MQTT Service
*A Step‑by‑Step Guide for Students and Developers*

This guide explains how to:

1. Create a HiveMQ Cloud account  
2. Create a Cloud MQTT Cluster  
3. Create MQTT credentials (username + password)  
4. Retrieve connection details  
5. Test your connection with the Web Client  

HiveMQ Cloud provides a free tier suitable for teaching labs and small IoT deployments.  
The process is based on HiveMQ’s official “Getting Started” documentation.

---

## 1. Sign Up for HiveMQ Cloud

1. Go to **https://console.hivemq.cloud**
2. Click **Sign Up**
3. Choose a login method: Email, GitHub, Google, or LinkedIn
4. Confirm your email (if you signed up via email)
5. Complete your user profile

HiveMQ automatically creates an **Organization** for you.

> Insert here a screeshot of your landing page.
---

## 2. Create a New HiveMQ Cloud Cluster

1. Log into the console: https://console.hivemq.cloud
2. Select **Clusters** in the left navigation
3. Click **Create Cluster**
4. Choose a **Cluster Name** (e.g., `MyFirstCluster`)
5. Select a **Region**
6. Choose a Plan: **Free / Starter**
7. Click **Create**

Cluster deployment takes **2–3 minutes**.

> Insert a screenshot of your cluster

---

## 3. Create MQTT Credentials

1. Open your Cluster
2. Go to **Access Management** / **Credentials**
3. Click **Add Credentials**
4. Create a **username** and **password**
5. Save your credentials

You may create one per student or per device.

---

## 4. Retrieve Your MQTT Connection Details

Your cluster dashboard shows:

```
Host:     yourclusterid.s1.eu.hivemq.cloud
Port:     8883 (TLS)
Username: your_username
Password: your_password
```

These values are used in your MQTT scripts.

---

## 5. Test the Broker with the HiveMQ Web Client

1. Inside your cluster page, open **Web Client**
2. Fill in:
   - Host
   - Port: 8883
   - Client ID
   - Username
   - Password
3. Click **Connect**
4. Subscribe to a topic: `test/topic`
5. Publish a message to the same topic

You should see your message appear immediately.

> Insert a screenshot of this step.

---

## 6. Summary

After setup, you now have:

| Component | Description |
|----------|-------------|
| **Cluster** | Fully hosted MQTT broker |
| **Host URL** | Needed for connecting devices |
| **Port 8883** | Secure TLS MQTT port |
| **Credentials** | Authentication for your MQTT clients |
| **Web Client** | Browser-based MQTT testing |

You can now connect IoT devices such as Raspberry Pi, ESP32, Node‑RED, or Python clients.
