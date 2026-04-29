# Kafka  Rider Stream 

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

<img width="1108" height="745" alt="Screenshot 2026-04-27 at 9 51 44 PM" src="https://github.com/user-attachments/assets/1a6ba1e9-71fc-47cc-a0ab-8f18c05b628a" />## 📁 Project Structure

```bash
kafka-crash-course/
├── client.js          # Kafka client configuration
├── admin.js           # Creates the Kafka topic
├── producer.js        # Interactive producer for location updates
├── consumer.js        # Consumer with group support
└── README.md
