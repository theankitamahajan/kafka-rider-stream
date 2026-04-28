# Kafka Crash Course 🚀

A hands-on, practical guide to learning **Apache Kafka** using **Node.js**, **Docker**, and the **kafkajs** library.

This project demonstrates core Kafka concepts like topics, partitions, producers, consumers, and consumer groups through a simple real-world example: **real-time rider location tracking**.

---

## 📌 Overview

This crash course helps you understand how Kafka works by building a small system where:
- A **producer** sends rider location updates ("north" or "south").
- Messages are partitioned based on location.
- Multiple **consumers** (in different groups) can consume these updates in real-time.

Perfect for beginners and intermediate developers who want to get comfortable with Kafka quickly.

---

## 🛠️ Tech Stack

- **Node.js** (Intermediate level recommended)
- **Apache Kafka** + **Zookeeper**
- **kafkajs** (Official Kafka client for Node.js)
- **Docker** (for running Kafka locally)
- **VS Code** (recommended)

---

## 🏗️ Architecture Diagram

```mermaid
flowchart TD
    subgraph "Producer"
        P[producer.js] 
    end

    subgraph "Apache Kafka Cluster"
        direction TB
        Z[Zookeeper] 
        B[Kafka Broker\n(port 9092)]
        
        subgraph "Topic: rider-updates"
            direction LR
            P0[Partition 0\n(North Riders)] 
            P1[Partition 1\n(South Riders)]
        end
        
        B --- Z
        B --- P0
        B --- P1
    end

    subgraph "Consumers"
        direction TB
        C1[consumer.js\nGroup: group1]
        C2[consumer.js\nGroup: group2]
        C3[consumer.js\nGroup: group3]
    end

    %% Data Flow
    P -->|"Sends messages\n(key: location-update)"| B
    P -.->|"north → Partition 0"| P0
    P -.->|"south → Partition 1"| P1

    P0 --> C1
    P0 --> C2
    P1 --> C1
    P1 --> C2
    P0 --> C3
    P1 --> C3

    style P fill:#4ade80,stroke:#166534
    style B fill:#60a5fa,stroke:#1e40af
    style P0 fill:#f472b6,stroke:#831843
    style P1 fill:#f472b6,stroke:#831843
    style C1 fill:#a5b4fc,stroke:#4338ca
    style C2 fill:#a5b4fc,stroke:#4338ca
    style C3 fill:#a5b4fc,stroke:#4338ca

## 📁 Project Structure

```bash
kafka-crash-course/
├── client.js          # Kafka client configuration
├── admin.js           # Creates the Kafka topic
├── producer.js        # Interactive producer for location updates
├── consumer.js        # Consumer with group support
└── README.md
