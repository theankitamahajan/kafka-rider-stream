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
## 🏗️ Architecture Diagram

```mermaid
flowchart TD
    %% Producer
    subgraph "Producer Application"
        Producer[producer.js<br/>Interactive Producer]
    end

    %% Kafka Cluster
    subgraph "Apache Kafka Cluster [Docker]"
        direction TB
        Z[Zookeeper<br/>Port: 2181]
        Broker[Kafka Broker<br/>Port: 9092]

        subgraph "Topic: rider-updates"
            direction LR
            P0[Partition 0<br/>North Riders<br/>Offset: ...]
            P1[Partition 1<br/>South Riders<br/>Offset: ...]
        end

        Broker --- Z
        Broker --> P0
        Broker --> P1
    end

    %% Consumers
    subgraph "Consumer Applications"
        direction TB
        CG1[Consumer<br/>Group: group1<br/>consumer.js]
        CG2[Consumer<br/>Group: group2<br/>consumer.js]
        CG3[Consumer<br/>Group: group3<br/>consumer.js]
    end

    %% Data Flow
    Producer -->|"1. Produces messages<br/>(JSON payload + key)"| Broker
    Producer -.->|"north → Partition 0"| P0
    Producer -.->|"south → Partition 1"| P1

    P0 & P1 -->|"2. Messages delivered to<br/>all consumer groups"| CG1
    P0 & P1 -->|"2. Messages delivered to<br/>all consumer groups"| CG2
    P0 & P1 -->|"2. Messages delivered to<br/>all consumer groups"| CG3

    %% Styling
    classDef producer fill:#4ade80,stroke:#166534,stroke-width:2px,color:#111
    classDef broker fill:#60a5fa,stroke:#1e40af,stroke-width:2px,color:#111
    classDef topic fill:#f472b6,stroke:#831843,stroke-width:2px,color:#111
    classDef consumer fill:#a5b4fc,stroke:#4338ca,stroke-width:2px,color:#111

    class Producer producer
    class Broker,Z broker
    class P0,P1 topic
    class CG1,CG2,CG3 consumer

## 📁 Project Structure

```bash
kafka-crash-course/
├── client.js          # Kafka client configuration
├── admin.js           # Creates the Kafka topic
├── producer.js        # Interactive producer for location updates
├── consumer.js        # Consumer with group support
└── README.md
