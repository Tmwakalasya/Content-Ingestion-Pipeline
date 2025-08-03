# Content Ingestion & Processing Pipeline

A resilient, scalable, and asynchronous system for ingesting and processing files using a Java-based microservices architecture. This project is designed to handle file uploads efficiently by offloading large data transfers and decoupling the initial upload from backend processing using a message queue.

---

## Architecture

This system is composed of two primary microservices, decoupled by a message queue, to handle the ingestion and processing flow.

<img width="3570" height="2357" alt="Blank board" src="https://github.com/user-attachments/assets/e44269b7-1024-4882-a4a4-eeb62401aa44" />


## Tech Stack

* **Language:** Java 17
* **Framework:** Spring Boot 3
* **Build Tool:** Maven
* **Cloud Services:**
    * AWS S3 (Simple Storage Service)
    * AWS SQS (Simple Queue Service)
* **Containerization:** Docker & Docker Compose

---

## Getting Started

Follow these instructions to get the project up and running on your local machine.

### Prerequisites

Make sure you have the following software installed:
* Java JDK 17 or later
* Apache Maven
* Docker and Docker Compose
* AWS CLI (with your credentials configured)

### Running the Application

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Tmwakalasya/Content-Ingestion-Pipeline
    cd content-ingestion-pipeline
    ```

2.  **Configure AWS Credentials:**
    Before running the application, you need to provide your AWS credentials to the services. Add the following to the `application.properties` file in both the `upload-service` and `processing-service` directories (`src/main/resources/application.properties`):

    ```properties
    # AWS Configuration
    cloud.aws.credentials.access-key=YOUR_ACCESS_KEY
    cloud.aws.credentials.secret-key=YOUR_SECRET_KEY
    cloud.aws.region.static=us-east-1
    ```

3.  **Build and Run with Docker Compose:**
    The easiest way to run the entire system is with Docker Compose. This command will build the Docker images for both services and start them.

    ```bash
    docker-compose up --build
    ```

4.  **Test the Endpoint:**
    Once the services are running, you can test the upload functionality. Use an API client like Postman to send a **POST** request with a `multipart/form-data` body containing a file to:

    `http://localhost:8080/upload`

    You should receive a `200 OK` response. You can then check your S3 bucket and SQS queue in the AWS Console to see the results.

---

## Project Structure

This project uses a **monorepo** structure, with each microservice contained in its own directory:

```
/
├── upload-service/       # Handles API requests and S3 URL generation
├── processing-service/   # Background worker that consumes from SQS
├── docker-compose.yml    # Orchestrates the services
└── README.md             # This file
```
