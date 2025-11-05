Perfect 👌 — since your backend is a **microservices-based salon booking system** running with **Spring Boot + Eureka + Keycloak + RabbitMQ + MySQL**, I’ll create a **professional `README.md`** you can upload directly to GitHub.

It will include:

* System overview
* Tech stack
* Architecture diagram (Markdown-based)
* Setup instructions (local + Docker)
* Health check URLs
* Common troubleshooting tips

---

## 🧾 **README.md**

````markdown
# 💇‍♀️ Salon Booking System (Microservices Architecture)

A production-ready **Salon Booking System** built using **Spring Boot**, **Spring Cloud**, **Eureka Discovery**, **Keycloak**, **RabbitMQ**, and **MySQL** — fully containerized with **Docker Compose**.

This system supports **user registration, salon management, service listings, payment handling, notifications, and reviews**, with a unified gateway and centralized service registry.

---

## 🏗️ Architecture Overview

```mermaid
graph TD
    A[Gateway Server] --> B[Eureka Server]
    A --> C[User Service]
    A --> D[Salon Service]
    A --> E[Service Offering Service]
    A --> F[Payment Service]
    A --> G[Notification Service]
    A --> H[Review Service]
    C --> I[(Shared MySQL)]
    C --> J[RabbitMQ]
    A --> K[Keycloak]
````

---

## 🧰 Tech Stack

| Category          | Technology                  |
| ----------------- | --------------------------- |
| Backend Framework | Spring Boot (v3.x)          |
| Service Discovery | Spring Cloud Netflix Eureka |
| API Gateway       | Spring Cloud Gateway        |
| Authentication    | Keycloak (OpenID Connect)   |
| Messaging         | RabbitMQ                    |
| Database          | MySQL (shared instance)     |
| Containerization  | Docker & Docker Compose     |
| Build Tool        | Maven                       |
| Monitoring        | Spring Boot Actuator        |

---

## 🚀 Microservices Overview

| Service                      | Port    | Description                                            |
| ---------------------------- | ------- | ------------------------------------------------------ |
| **Eureka Server**            | `8070`  | Service registry for microservices                     |
| **Gateway Server**           | `5000`  | API gateway routing all external requests              |
| **User Service**             | `5001`  | Handles user registration, authentication, and profile |
| **Salon Service**            | `5002`  | Manages salons and related info                        |
| **Service Offering Service** | `5005`  | Handles salon services and pricing                     |
| **Payment Service**          | `5006`  | Manages payment processing and history                 |
| **Notification Service**     | `5007`  | Sends emails and notifications                         |
| **Review Service**           | `5008`  | Stores and manages customer reviews                    |
| **Keycloak**                 | `7080`  | Authentication and authorization server                |
| **RabbitMQ (Mgmt)**          | `15672` | Message broker management dashboard                    |
| **MySQL (Shared)**           | `3306`  | Central database instance for all services             |

---

## ⚙️ Setup Instructions

### 🧩 Prerequisites

Make sure you have:

* **Docker** ≥ 24.x
* **Docker Compose** ≥ 2.x
* **JDK 17+** (for building)
* **Maven** (for local builds, optional)

---

### 🐳 Run with Docker Compose (Recommended)

1. Clone this repository:

   ```bash
   git clone https://github.com/<your-username>/salon-booking-backend.git
   cd salon-booking-backend
   ```

2. Build Docker images (if not already pushed):

   ```bash
   mvn clean package -DskipTests
   docker build -t zosh/salon-user:v1 -f user/Dockerfile .
   docker build -t zosh/salon-salon:v1 -f salon/Dockerfile .
   # (repeat for other services)
   ```

3. Start the full stack:

   ```bash
   docker-compose up -d
   ```

4. Verify containers:

   ```bash
   docker ps
   ```

5. Visit the dashboards:

   * **Eureka Dashboard:** [http://localhost:8070](http://localhost:8070)
   * **API Gateway:** [http://localhost:5000](http://localhost:5000)
   * **Keycloak Admin Console:** [http://localhost:7080](http://localhost:7080)

     * Username: `admin`
     * Password: `admin`
   * **RabbitMQ Dashboard:** [http://localhost:15672](http://localhost:15672)

     * Username: `guest`
     * Password: `guest`

---

### 🧑‍💻 Run Locally (for Development)

You can run only the infrastructure services in Docker:

```bash
docker-compose up -d shared-mysql rabbit eurekaserver keycloak
```

Then run your desired microservice from IntelliJ/VSCode using:

```bash
mvn spring-boot:run
```

Make sure your `application.yml` points to:

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/salon_userdb
    username: root
    password: Akash468@
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8070/eureka/
```

---

## 🔍 Health Check Endpoints

| Service           | Health URL                   |
| ----------------- | ---------------------------- |
| Gateway           | `/actuator/health`           |
| Eureka            | `/actuator/health`           |
| All Microservices | `/{service}/actuator/health` |

You can test with:

```bash
curl http://localhost:5001/actuator/health
```

---

## 🩺 Monitoring & Observability

Spring Boot Actuator is enabled in all services.
You can use:

* `/actuator/health`
* `/actuator/info`
* `/actuator/env`
* `/actuator/metrics`

---

## 🧱 Database Schema Strategy

All services share the **same MySQL container** (`shared-mysql`) but use **different databases**:

* `salon_userdb`
* `salondb`
* `salon_servicedb`
* `salon_paymentdb`
* `salon_notificationdb`
* `salon_reviewdb`

---

## 🧾 License

This project is licensed under the [MIT License](LICENSE).

---

## 👨‍💻 Author

**Akash (Zosh Project)**

> A modular, scalable salon booking system for modern distributed environments.

---

## 💡 Troubleshooting

| Issue                    | Cause                    | Fix                                       |
| ------------------------ | ------------------------ | ----------------------------------------- |
| `eurekaserver unhealthy` | Service startup delay    | Run `docker-compose restart eurekaserver` |
| Services not registered  | Eureka not fully started | Wait 20–30s after startup                 |
| DB connection error      | MySQL not ready yet      | Restart dependent containers              |
| Keycloak not reachable   | Port conflict or delay   | Check port 7080 or container logs         |

---

## 🧭 Future Improvements

* Add centralized configuration via **Spring Cloud Config Server**
* Add distributed tracing with **Zipkin / Sleuth**
* Add monitoring via **Prometheus + Grafana**

---

🚀 **Ready to run:**

```bash
docker-compose up -d
```

🟢 Check [http://localhost:8070](http://localhost:8070) → You’ll see all microservices registered!

```

