# Overview
This project demonstrates the containerization and deployment of a full-stack YOLO application using Docker. The application features both front-end and back-end services, with seamless integration to a cloud-hosted MongoDB database for secure data storage.

# Requirements
Ensure Docker is installed on your system. You can install Docker using the official guide:  
- [Docker Installation Guide](https://docs.docker.com/engine/install/)

# How to Launch the Application
To start the application, run the following command in the project directory:  
```bash
docker compose up

# This will start the container for the back-end service.

# Notes
This command launches only the backend of the application. You will need to launch the front-end service separately.
The application is configured to use a cloud MongoDB database, ensuring that all data is securely stored and accessible from anywhere.
