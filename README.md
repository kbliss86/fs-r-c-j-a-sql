# Project Name: Full Stack React with C#/Java API & Azure SQL

## Overview
This project is a full-stack web application that leverages a **React Frontend** and a **C# (ASP.NET) or Java (Spring Boot) Backend** API to interact with an **SQL Database hosted in Azure**. This README will guide you through setting up and running the project, covering all aspects including environment configuration, database setup, and API connections.

## Table of Contents
1. [Project Structure](#project-structure)
2. [Technologies Used](#technologies-used)
3. [Getting Started](#getting-started)
4. [Database Setup](#database-setup)
5. [Backend Setup](#backend-setup)
   - [C# (ASP.NET Core)](#csharp-aspnet-core-backend-setup)
   - [Java (Spring Boot)](#java-spring-boot-backend-setup)
6. [Frontend Setup](#frontend-setup)
7. [Running the Application](#running-the-application)
8. [Deployment](#deployment)
9. [Troubleshooting](#troubleshooting)

## Project Structure
```
root/
  |-- backend/
  |    |-- csharp-api/ (C# Backend)
  |    |-- java-api/ (Java Backend)
  |
  |-- frontend/
  |    |-- react-app/ (React Frontend)
  |
  |-- database/
       |-- scripts/ (SQL scripts for Azure SQL Database)
```

## Technologies Used
- **Frontend**: React.js
- **Backend**: ASP.NET Core (C#) or Spring Boot (Java)
- **Database**: Azure SQL Database
- **Hosting**: Azure (for SQL and optionally the backend)
- **Other**: REST APIs, Entity Framework (C#), JPA (Java), Axios, Docker

## Getting Started
To get started with the project, you'll need to set up your development environment.

### Prerequisites
- **Node.js** (for the React frontend) - [Download here](https://nodejs.org/)
- **.NET SDK** (for the C# API) - [Download here](https://dotnet.microsoft.com/download)
- **Java JDK** (for the Java API) - [Download here](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- **Azure CLI** - [Download here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- **SQL Server Management Studio (SSMS)** or **Azure Data Studio** - [Download here](https://aka.ms/ssmsfullsetup)

## Database Setup
1. **Create Azure SQL Database**
   - Log in to your Azure account and create a new **Azure SQL Database**.
   - Note down the connection string and credentials.

2. **Configure Database**
   - Use **SQL Server Management Studio** (SSMS) or **Azure Data Studio** to connect to your Azure SQL instance.
   - Run the provided scripts from `database/scripts/` to create the required tables and populate them with sample data.

   ```sql
   CREATE TABLE SampleTable (
     ID INT PRIMARY KEY IDENTITY,
     Name VARCHAR(100),
     Description TEXT
   );
   INSERT INTO SampleTable (Name, Description) VALUES ('Sample Name', 'Sample Description');
   ```

## Backend Setup
You can choose either the C# or Java backend.

### C# (ASP.NET Core) Backend Setup
1. **Navigate to the C# Backend Directory**
   ```sh
   cd backend/csharp-api
   ```
2. **Restore Dependencies**
   ```sh
   dotnet restore
   ```
3. **Configure Database Connection**
   - In `appsettings.json`, update the connection string to point to your Azure SQL Database:
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "<Your Azure SQL Connection String>"
   }
   ```
4. **Run the Backend**
   ```sh
   dotnet run
   ```

### Java (Spring Boot) Backend Setup
1. **Navigate to the Java Backend Directory**
   ```sh
   cd backend/java-api
   ```
2. **Install Dependencies**
   ```sh
   ./mvnw install
   ```
3. **Configure Database Connection**
   - In `application.properties`, update the database connection settings:
   ```properties
   spring.datasource.url=jdbc:sqlserver://<your-server>.database.windows.net:1433;database=<your-database>
   spring.datasource.username=<your-username>
   spring.datasource.password=<your-password>
   ```
4. **Run the Backend**
   ```sh
   ./mvnw spring-boot:run
   ```

## Frontend Setup
1. **Navigate to the React Directory**
   ```sh
   cd frontend/react-app
   ```
2. **Install Dependencies**
   ```sh
   npm install
   ```
3. **Configure API Endpoint**
   - In `.env`, specify the backend API endpoint (either the C# or Java backend):
   ```env
   REACT_APP_API_URL=http://localhost:5000/api
   ```
4. **Run the Frontend**
   ```sh
   npm start
   ```

## Running the Application
1. **Run the Backend**: Follow the steps for either C# or Java backend to start the API.
2. **Run the Frontend**: Start the React app using `npm start`.
3. **Access the Application**: Open your browser and go to `http://localhost:3000` to see the frontend interface.

## Deployment
### Deploying the SQL Database
- **Azure SQL Database** is already hosted in Azure. Ensure all necessary tables are created.

### Deploying the Backend API
- You can use **Azure App Service** or **Docker** to deploy the backend.
- For **ASP.NET Core**:
  ```sh
  az webapp up --name <your-app-name> --resource-group <your-resource-group> --sku F1
  ```
- For **Java Spring Boot**:
  ```sh
  az webapp up --name <your-app-name> --runtime "JAVA|11" --resource-group <your-resource-group> --sku F1
  ```

### Deploying the React Frontend
- Use a service like **Netlify**, **Vercel**, or **Azure Static Web Apps** for deployment.
  ```sh
  npm run build
  # Then deploy the `build/` folder to your hosting service.
  ```

## Troubleshooting
1. **Database Connection Issues**
   - Ensure that your Azure SQL Database allows connections from your IP (configure the **Firewall settings**).
   - Double-check the connection strings in both the backend projects.

2. **CORS Errors**
   - If you encounter CORS errors when making API calls from the frontend, ensure you add CORS support in the backend:
     - **ASP.NET Core**: Add `services.AddCors()` in `Startup.cs`.
     - **Spring Boot**: Use `@CrossOrigin` annotation on the controller.

3. **Environment Variables**
   - Ensure `.env` files are properly configured in both backend and frontend for local development.

## Contributing
Feel free to fork this repository and make contributions. Create a pull request for any major changes.

## License
This project is licensed under the MIT License.

