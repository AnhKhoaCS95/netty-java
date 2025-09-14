Project Features and Functionality

This project is a secure chat application built using Java and Netty with both server and client implementations. It provides encrypted communication, group messaging, and integrated utilities like subdomain scanning and weather information retrieval.

1. Chat System
a. Broadcast Chat (Global Chat)

Messages are sent to all connected clients who are not in a group.

Ideal for general announcements or global conversations.

Implemented in the broadcast() method of the NettyServer class.

Example:

Alice: Hello everyone!

b. Multicast Chat (Group Chat)

Clients can join or leave specific chat groups using commands:

@join:<group_name> → join a group.

@leave → leave the current group and return to global chat.

Messages sent within a group are only visible to group members.

Implemented using the clientGroups map to track which user belongs to which group.

2. Secure Communication (Encryption & Digital Signature)

The chat system uses hybrid encryption for secure messaging between the client and server:

a. RSA (Asymmetric Encryption)

Used during the initial handshake to securely exchange the AES session key.

Server sends its public key to the client.

Client encrypts a randomly generated AES key with the server's public key.

b. AES (Symmetric Encryption)

After the handshake, all chat messages are encrypted using AES-CBC-256.

Each message includes:

Encrypted text

IV (Initialization Vector)

Both are sent with the prefix [ENCRYPTED_MSG].

c. Digital Signatures

Clients sign messages using their private RSA key.

The server verifies signatures with the client’s public key to ensure:

Message integrity (no tampering).

Sender authenticity (identity verification).

This approach provides end-to-end encryption with authentication, preventing eavesdropping or spoofing.

3. Subdomain Scanning Feature

Clients can request the server to scan the top 100 subdomains of a given domain.

Command:

@scan:<domain>


Example:

@scan:example.com


The server attempts DNS resolution for common subdomains (from a public SecLists wordlist).

Found subdomains are returned to the requesting client in real time.

Use case: basic penetration testing or network reconnaissance.

4. Weather Information Retrieval

Clients can request current weather data for a specific city.

Command:

@weather:<city_name>


Example:

@weather:London


The server:

Uses the Open-Meteo Geocoding API to get the city's latitude and longitude.

Fetches current weather conditions (temperature, wind speed, timestamp) from the Open-Meteo Weather API.

Results are securely sent back to the client.

Example Output:

📍 Weather in London:
- Time: 2025-09-14T10:00:00Z
- Temperature: 18.5°C
- Wind Speed: 3.2 m/s

5. Database Logging

All chat messages are saved to a database using DBUtil.saveMessageToDatabase().

Stored fields include:

Sender

Receiver (group name or "global")

Message content

This ensures message history can be audited or restored later.

Technical Stack

Language: Java

Networking Library: Netty

Cryptography: RSA & AES (Java Cryptography Extension - JCE)

Database: Configurable via DBUtil

API Integration:

Open-Meteo Geocoding API

Open-Meteo Weather API

External Resources:

Subdomain wordlist from SecLists GitHub repository.

Example Commands for Clients
Command	Description
@join:group1	Join the group named group1
@leave	Leave the current group and return to global chat
@scan:domain.com	Scan top 100 subdomains of domain.com
@weather:London	Get current weather for London
Security Workflow

Initial Connection:

Server sends its RSA public key to the client.

Key Exchange:

Client generates a temporary AES key and securely sends it using RSA encryption.

Digital Signature:

Client signs the first message (username) with its private key.

Server verifies the signature and establishes a secure session.

Secure Messaging:

All chat messages are encrypted using AES-CBC.

Each message includes a unique IV for added security.


*Problem Solving:

This project tackles secure communication, group messaging, and network utilities in one chat application.

1. Secure Messaging

Problem: Plain text messages are vulnerable to attacks.

Solution:

RSA for secure key exchange.

AES-CBC for fast message encryption.

Digital signatures to verify sender identity.

Result: Encrypted, verified, and tamper-proof chat messages.

2. Broadcast & Group Chat

Problem: Hard to manage global and group chats efficiently.

Solution:

@join:<group> → join a group.

@leave → return to global chat.

Smart routing sends messages only to relevant users.

Result: Smooth broadcast and multicast communication.

3. Built-in Tools

Subdomain Scanner: @scan:<domain> → Finds top 100 hidden subdomains.

Weather Info: @weather:<city> → Real-time weather using Open-Meteo API.

4. Reliability & Performance

Database logging to save all messages.

Netty non-blocking I/O for high scalability.

Thread-safe structures to prevent race conditions.




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
