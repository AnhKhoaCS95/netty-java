# 🔐 Secure Chat System with Multicast, Encryption, and Utilities

A **Java-based chat application** with **broadcast**, **multicast (group chat)**, and **end-to-end encryption**.  
It also includes built-in **subdomain scanning** and **real-time weather lookup** utilities.  
The project uses **Netty** for high-performance, non-blocking I/O and **MySQL** for message storage.

---

![e31b752875679b64fce009922f9f0dda](https://github.com/user-attachments/assets/5e159848-2251-4c50-8a00-8c2b3beb0f53)

## 🚀 Features

### **1. Secure Messaging**
- **RSA** for secure key exchange.
- **AES-CBC** for fast and secure message encryption.
- **Digital Signatures** to verify sender identity and prevent tampering.
- **Result:** Messages are encrypted, verified, and tamper-proof.

---

### **2. Broadcast & Group Chat**
- **Broadcast Chat:**  
  Send messages to all connected users.
- **Multicast (Group Chat):**  
  - `@join:<group>` → Join a group.  
  - `@leave` → Leave group and return to global chat.  
  - Smart message routing ensures only group members receive group messages.

---

### **3. Built-in Tools**
- **Subdomain Scanner:**  
  `@scan:<domain>` → Find top hidden subdomains for security testing.
- **Weather Lookup:**  
  `@weather:<city>` → Fetch real-time weather data using the **Open-Meteo API**.

---

### **4. Reliability & Performance**
- **MySQL Database Logging:** All chat messages are securely stored.
- **Netty Non-Blocking I/O:** Highly scalable and efficient for multiple concurrent users.
- **Thread-Safe Data Structures:** Prevents race conditions when handling messages and groups.

---

## 🛠️ Tech Stack

- **Language:** Java (JDK 17+)
- **Networking:** Netty
- **Database:** MySQL
- **Encryption:**
  - RSA (2048-bit) for secure key exchange.
  - AES-CBC (128-bit) for fast message encryption.
- **UI:** Java Swing (for client and server interfaces)
- **API:** Open-Meteo (for weather data)

---

## 📂 Project Structure

src/
├── DBUtil.java # Database utility (MySQL connection, password hashing)

├── Home.form # UI layout for Home page

├── Home.java # Logic for Home page

├── LoginFormModern.java # Modern login form

├── SignUpFormModern.java # Modern sign-up form

├── NettyClient.java # Client-side networking and encryption

├── NettyServer.java # Server-side networking and message handling

├── Server.form # UI layout for server monitor

├── Server.java # Server application with GUI


---

## ⚡ How It Works

### **1. Encryption Flow**
1. **RSA Key Exchange:**  
   - Server shares its **public key** with the client.  
   - Client generates a random **AES key**, encrypts it using RSA, and sends it to the server.
2. **AES Encryption for Messages:**  
   - Once the AES key is exchanged, all chat messages are encrypted with **AES-CBC** for speed and security.
3. **Digital Signatures:**  
   - Messages are signed using the sender's private key to prevent tampering.

---

### **2. Group Chat Flow**
- Users can dynamically join or leave groups:
  - `@join:team1` → joins "team1".
  - `@leave` → exits the group and returns to broadcast mode.
- Messages sent in a group are **only delivered to group members**.

---

## 🧩 Example Commands

| Command            | Description                               |
|--------------------|-------------------------------------------|
| `@join:devs`       | Join the "devs" group                     |
| `@leave`           | Leave current group                       |
| `@scan:example.com`| Scan domain for subdomains                |
| `@weather:London`  | Get real-time weather for London          |

---

## 📊 Problem Solving

This project addresses several challenges:

### **1. Secure Messaging**
- **Problem:** Plain text messages are vulnerable to eavesdropping and tampering.  
- **Solution:**  
  - RSA for secure key exchange.  
  - AES-CBC for fast encryption.  
  - Digital signatures for sender verification.
- **Result:** Fully encrypted and verified chat messages.

---

### **2. Broadcast & Group Chat**
- **Problem:** Managing global and group chats efficiently.  
- **Solution:**  
  - Group-based routing to send messages only to relevant users.  
  - Easy commands for joining/leaving groups.
- **Result:** Smooth **broadcast** and **multicast** communication.

---

### **3. Built-in Utilities**
- **Problem:** Users often need quick external tools without leaving the chat.  
- **Solution:**  
  - Subdomain scanner to assist with penetration testing.  
  - Real-time weather lookup using public API.
- **Result:** Extra tools integrated directly into the chat.

---

### **4. Reliability & Performance**
- **Problem:** Handling multiple clients and preventing data loss.  
- **Solution:**  
  - Netty for scalable, non-blocking I/O.  
  - MySQL database to persist chat history.  
  - Thread-safe structures for concurrency safety.

---

## 🚀 Getting Started

### **1. Prerequisites**
- Java 17+
- MySQL 8.0+
- Maven (for dependency management)

### **2. Database Setup**
Run the following SQL to create the database and messages table:


run server first then login

Database:

CREATE TABLE users (
    id INT(11) AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    address VARCHAR(255) DEFAULT NULL,
    phone VARCHAR(20) DEFAULT NULL,
);

CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sender VARCHAR(255),
    receiver VARCHAR(255),
    content TEXT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
);



//DEMO

![Image](https://github.com/user-attachments/assets/154d120d-4e75-4bc5-affb-ae5f78ca0fd4)

https://www.youtube.com/watch?v=l1C9XMt4qfs





