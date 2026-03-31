# 📌 Services - Enterprise Cloud Application (ECA) Business Services Layer

The **Services layer** represents the core business logic of the Enterprise Cloud Application (ECA). It consists of independently deployable microservices responsible for managing students, academic programs, and enrollments within a distributed cloud-based system.

---

## 👩‍🎓 Student Information

| Field          | Value                                 |
| -------------- | ------------------------------------- |
| Student Name   | Kavindi Sathsarani Manimendra         |
| Student Number | 2301692042                            |
| Slack Handle   | @kavindi sathsarani                   |
| Module         | ITS 2130 Enterprise Cloud Application |
| Program        | GDSE @ IJSE                           |
| GCP Project ID | it-assignment-3                       |

---

## 📖 About

This project is developed as part of the **Enterprise Cloud Application (ECA)** module in the GDSE program at IJSE.

The Services layer focuses on implementing **domain-driven microservices** that handle the core functionalities of the system. Each service is designed to be **loosely coupled, independently deployable, and scalable**, following modern cloud-native architectural principles.

---

## 📌 Project Description

The system is built using a **microservices architecture**, where each service is responsible for a specific business domain:

* **Student-Service** → Manages student data and profiles
* **Program-Service** → Handles academic program details
* **Enrollment-Service** → Manages student enrollments

Each microservice:

* Runs independently
* Connects to the **Config Server** for configurations
* Registers with **Eureka Service Registry**
* Communicates through the **API Gateway**
* Uses REST APIs for interaction

---

## 🛠️ Technology Stack

| Technology           | Version  | Purpose               |
| -------------------- | -------- | --------------------- |
| Java                 | 25       | Programming Language  |
| Spring Boot          | 4.0.3    | Backend Framework     |
| Spring Cloud         | 2025.1.0 | Microservices Tools   |
| Eureka Client        | -        | Service Registration  |
| Config Client        | -        | Config Management     |
| Spring Data JPA      | Latest   | Database ORM          |
| PostgreSQL           | 15+      | Database              |
| MapStruct            | Latest   | DTO Mapping           |
| Lombok               | Latest   | Boilerplate Reduction |
| Spring Boot Actuator | Latest   | Monitoring            |
| GCP                  | -        | Cloud Deployment      |

---

## 🧩 Services Overview

### 🔹 Student-Service (Port: 8000)

**Purpose:** Manage student information

**Features:**

* CRUD operations for students
* Profile picture upload
* NIC validation
* Contact management

---

### 🔹 Program-Service (Port: 8001)

**Purpose:** Manage academic programs

**Features:**

* Create and manage programs
* Handle program duration and credits
* Maintain curriculum data

---

### 🔹 Enrollment-Service (Port: 8002)

**Purpose:** Manage enrollments

**Features:**

* Enroll students in programs
* Track enrollment details
* Validate relationships between students and programs

---

## 🏗️ Architecture Overview

```
Client → API Gateway → Microservices
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
 Student-Service  Program-Service  Enrollment-Service
        │              │              │
        └──────────────┴──────────────┘
                      ▼
                PostgreSQL DB
```

---

## ⚙️ Setup / Getting Started

### 🔹 Prerequisites

* Java 17+ / 25
* Maven
* PostgreSQL
* Git
* Platform services (Config Server + Eureka) running

---

### 🔹 Clone Repository

```bash
git clone --recursive https://github.com/kavindisathsarani/Capstone-Project-Platform.git
cd Services
```

---

### 🔹 Build Services

```bash
mvn clean install
```

---

### 🔹 Run Services (After Platform)

```bash
# Student-Service
cd Student-Service
mvn spring-boot:run

# Program-Service
cd ../program-Service
mvn spring-boot:run

# Enrollment-Service
cd ../Enrollment-Service
mvn spring-boot:run
```

---

## 🔄 Startup Order

1. PostgreSQL
2. Config Server (9000)
3. Service Registry (9001)
4. Student-Service (8000)
5. Program-Service (8001)
6. Enrollment-Service (8002)
7. API Gateway (7000)

---

## 🌐 Access Services

### Direct Access

```bash
http://localhost:8000/api/v1/students
http://localhost:8001/api/v1/programs
http://localhost:8002/api/v1/enrollments
```

### Through API Gateway

```bash
http://localhost:7000/api/v1/students
http://localhost:7000/api/v1/programs
http://localhost:7000/api/v1/enrollments
```

---

## 🧪 Health Check

```bash
curl http://localhost:8000/actuator/health
curl http://localhost:8001/actuator/health
curl http://localhost:8002/actuator/health
```

---

## 🌐 Eureka Dashboard

**Local:**

```
http://localhost:9001
```

**GCP (Live):**

```
http://34.126.173.115:9001  
http://34.142.245.4:9001  
http://35.240.148.114:9001  
```

---

## 🗄️ Database Configuration

```
Host: localhost  
Port: 12500  
Database: eca  
```

---

## 📊 Monitoring

* `/actuator/health`
* `/actuator/metrics`
* `/actuator/env`

---

## ☁️ GCP Deployment (VM + SSH)

Services are deployed using **Google Cloud Compute Engine (VM instances)** and managed via SSH.

```bash
# Connect to VM
gcloud compute ssh <vm-name>

# Run service
java -jar target/*.jar

# Run with PM2
pm2 start ecosystem.config.js
```

---

## 🛠️ Troubleshooting

### Service Not Registering

* Ensure Config Server & Eureka are running

### Database Error

* Check PostgreSQL is running on port 12500

### 503 Error

* Verify services are registered in Eureka

---

## 📌 Status

✅ Running on GCP VM (SSH Deployment)

---
