# Table Talk - Bar & Restaurant Management System

<div align="center">
  <p>
    <a href="https://github.com/gorocode/tt-react">Frontend Repository</a> •
    <a href="https://github.com/gorocode/tt-spring">Backend Repository</a> •
  </p>
</div>

<div align="center">
  <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring&logoColor=white" alt="Spring Boot" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL" />
</div>

<div align="center">
  <h3><a href="https://tt.gorocode.dev/manager" target="_blank">🔗 Live Demo</a></h3>
  <p>Demo credentials (all with password <code>Password1234$</code>):</p>
  <table>
    <tr>
      <td><strong>Username</strong></td>
      <td><strong>Role</strong></td>
    </tr>
    <tr>
      <td><code>admin</code></td>
      <td>Administrator (full access)</td>
    </tr>
    <tr>
      <td><code>manager</code></td>
      <td>Manager (reporting and management)</td>
    </tr>
    <tr>
      <td><code>worker</code></td>
      <td>Staff (day-to-day operations)</td>
    </tr>
  </table>
</div>

## 📋 Overview

Table Talk is a comprehensive bar and restaurant management application designed to streamline daily operations, from table and order management to menu and product customization. The application consists of a React/TypeScript frontend and a Spring Boot backend, all orchestrated via Docker Compose for easy deployment.

---

## ✨ Features

- **Interactive Table Management**: Visualize and manage tables with dynamic, customizable layouts
- **Comprehensive Order Handling**: Create, split, merge, and track orders in real-time
- **Complete Menu System**: Organize menus with categories, products, and allergen information
- **Real-time Communication**: Instant kitchen notifications via WebSockets
- **Invoicing & Payments**: Generate invoices and process payments through multiple methods
- **Customizable UI**: Theme system for adapting the interface to your needs
- **Role-Based Access**: Different interfaces for management, bar staff, and kitchen staff

## 🛠️ Technology Stack

### Frontend
- **Framework**: React with TypeScript
- **Styling**: TailwindCSS for responsive design
- **Build Tool**: Vite for fast development
- **State Management**: React Context API
- **Real-time**: StompJS for WebSocket communication

### Backend
- **Framework**: Spring Boot (Java)
- **API Style**: RESTful architecture
- **Database**: PostgreSQL
- **Security**: Spring Security with JWT

### DevOps
- **Containerization**: Docker and Docker Compose
- **Deployment**: Cloud-based deployment with automated pipelines

---

## 🚀 Quick Start Guide

### Prerequisites
- Docker and Docker Compose installed on your system
- Git (optional, for cloning)

### Installation

1. **Get the Project**
   ```bash
   # Option 1: Clone using Git
   git clone https://gitlab.com/goromigue/tt-bar-manager.git
   cd tt-bar-manager
   
   # Option 2: Download ZIP from GitLab and extract to your preferred location
   ```

2. **Start the Application**
   ```bash
   # Make sure Docker Desktop is running
   docker-compose up --build
   ```
   This command builds and starts all containers (frontend, backend, and database).

3. **Access the Application**
   - Open your browser and navigate to [http://localhost:5173/manager](http://localhost:5173/manager)
   - Log in with default credentials:
     - Username: `admin`
     - Password: `Password1234$`

4. **Stopping the Application**
   ```bash
   # Press Ctrl+C in your terminal to stop services, then run:
   docker-compose down
   ```

### 🌐 Live Demo
A live demo is available at [https://tt.gorocode.dev](https://tt.gorocode.dev)

---

## 🗼 Project Structure

```
tt-bar-manager/
├── docker-compose.yml       # Orchestrates all services
├── README.md               # Main project documentation
├── API.md                  # API documentation
│
├── tt-spring/                # Backend (Spring Boot)
│   ├── Dockerfile          # Backend container configuration
│   ├── pom.xml             # Maven dependencies
│   ├── src/                # Source code
│   │   ├── main/java/com/goro/tabletalk/
│   │   │   ├── boot/       # Application bootstrapping
│   │   │   ├── config/     # Configuration classes
│   │   │   ├── controller/ # API endpoints
│   │   │   ├── dto/        # Data Transfer Objects
│   │   │   ├── entity/     # JPA entities
│   │   │   ├── mapper/     # Object mappers
│   │   │   ├── repository/ # Database access
│   │   │   └── service/    # Business logic
│   │   └── resources/      # Application properties
│   └── README.md           # Backend documentation
│
└── tt-react/               # Frontend (React)
    ├── Dockerfile          # Frontend container configuration
    ├── package.json        # npm dependencies
    ├── src/                # Source code
    │   ├── api/            # API services
    │   ├── components/     # UI components
    │   ├── context/        # React contexts
    │   ├── pages/          # Application pages
    │   └── utils/          # Helper functions
    └── README.md           # Frontend documentation
```

---

## 🔑 Environment Variables

### Frontend (.env)
```properties
VITE_API_URL=http://localhost:8080
VITE_WS_URL=ws://localhost:8080/
VITE_PAYPAL_ID=your-paypal-client-id
VITE_CLOUDINARY_NAME=your-cloudinary-name
VITE_CLOUDINARY_PRESENT=your-cloudinary-upload-preset
VITE_QR_SALT=tt-bar-manager
```

### Backend (application.properties)
The main configuration is handled through Spring Boot application properties and Docker environment variables.
```properties
FRONTEND_URL=http://localhost:5173
SPRING_DATASOURCE_URL=jdbc:postgresql://postgres-db:5432/tabletalk
SPRING_DATASOURCE_USERNAME=user
SPRING_DATASOURCE_PASSWORD=tableuser
SPRING_JPA_HIBERNATE_DDL_AUTO=update
SPRING_JPA_SHOW_SQL=false
JWT_SECRET=yourStrongSecretKeyHere
JWT_EXPIRATION_MS=86400000
```

### Database
Database credentials are configured in the `docker-compose.yml` file:
```properties
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=tabletalk
```

---

## 🔧 Troubleshooting

### Common Issues

- **Docker Services Not Starting**
  - Ensure Docker Desktop is running
  - Check if required ports (5173, 8080, 5432) are available
  - Try stopping existing containers: `docker-compose down`
  - Clear Docker cache: `docker system prune`

- **Frontend Not Connecting to Backend**
  - Verify environment variables in `.env`
  - Check backend logs for errors
  - Ensure backend is properly running on port 8080

- **Database Connection Issues**
  - Check PostgreSQL logs in Docker
  - Verify database credentials in `docker-compose.yml`
  - Ensure database initialization scripts are running correctly

---


## 🔒 Security

The application uses JWT (JSON Web Tokens) for authentication. Default credentials are provided for testing purposes only. In production, it is strongly recommended to change these credentials and implement proper security measures.

---

## 📀 License

This project is licensed under the MIT License - see the individual `LICENSE` files in each subproject for details.
