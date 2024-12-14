# API Application with JWT

A robust and secure API built with PHP, leveraging the Slim Framework and Firebase JWT for token-based authentication. This application facilitates secure user interactions with endpoints designed for token generation, user authentication, and scalable resource management.

## Table of Contents
- [Features](#features)
- [Setup](#setup)
- [SQL Database](#sql-database)
- [Technologies Used](#technologies-used)
- [API Endpoints](#api-endpoints)
  - [Authentication](#authentication)
  - [Resource Management](#resource-management)
  - [Sample Data Operations](#sample-data-operations)
- [Security Notes](#security-notes)

## Features
- **Token-Based Authentication**: Securely handle authentication with JWT.
- **CRUD Operations**: Efficient endpoints for managing users and resources.
- **Slim Framework Integration**: Lightweight and modular API design.
- **Secure Database Transactions**: Ensure data integrity and minimize vulnerabilities.

## Setup

1. Clone the repository:
   ```bash
   git clone [your-repository-url]
   cd [repository-name]
   ```

2. Install dependencies using Composer:
   ```bash
   composer install
   ```

3. Configure the database in the `config.php` file:
   ```php
   $db = [
       'host' => 'localhost',
       'username' => 'root',
       'password' => '',
       'dbname' => 'secure_api'
   ];
   ```

4. Set up the database schema:
   ```sql
   CREATE TABLE users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       username VARCHAR(255) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL
   );

   CREATE TABLE resources (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255),
       description TEXT
   );
   ```

5. Start the PHP development server:
   ```bash
   php -S localhost:8080
   ```

## SQL Database
The application uses MySQL for data persistence, with tables for managing users and resources. The database structure ensures scalability and secure interactions.

## Technologies Used
- **Backend**: PHP with Slim Framework
- **Database**: MySQL
- **Authentication**: Firebase JWT (JSON Web Tokens)
- **Dependencies**: PSR-7 HTTP Message Implementation

## API Endpoints

### Authentication

#### Register User
- **Endpoint**: `POST /register`
- **Request Body**:
   ```json
   {
     "username": "example_user",
     "password": "secure_password"
   }
   ```

#### Login User
- **Endpoint**: `POST /login`
- **Request Body**:
   ```json
   {
     "username": "example_user",
     "password": "secure_password"
   }
   ```
- **Response**:
   ```json
   {
     "token": "{{jwt-token}}"
   }
   ```

### Resource Management

#### Create Resource
- **Endpoint**: `POST /resource`
- **Headers**: `Authorization: Bearer {{jwt-token}}`
- **Request Body**:
   ```json
   {
     "name": "Resource Name",
     "description": "Detailed description"
   }
   ```

#### Retrieve All Resources
- **Endpoint**: `GET /resource`
- **Headers**: `Authorization: Bearer {{jwt-token}}`

#### Update Resource
- **Endpoint**: `PUT /resource/{id}`
- **Headers**: `Authorization: Bearer {{jwt-token}}`
- **Request Body**:
   ```json
   {
     "name": "Updated Resource Name",
     "description": "Updated description"
   }
   ```

#### Delete Resource
- **Endpoint**: `DELETE /resource/{id}`
- **Headers**: `Authorization: Bearer {{jwt-token}}`

### Sample Data Operations

#### Retrieve Resources with Metadata
- **Endpoint**: `GET /resource/metadata`
- **Headers**: `Authorization: Bearer {{jwt-token}}`
- **Response**:
   ```json
   [
     {
       "resource": "Resource Name",
       "metadata": "Metadata details"
     }
   ]
   ```

## Security Notes
- Always use HTTPS in production to prevent token interception.
- Store passwords securely using a hashing algorithm like bcrypt.
- Rotate the JWT secret key periodically to enhance security.
- Implement input validation to prevent SQL injection and other attacks.
- Employ rate limiting to mitigate brute force attempts.

## Additional Resources
- [Slim Framework Documentation](https://www.slimframework.com/docs/)
- [Firebase JWT Documentation](https://github.com/firebase/php-jwt)
- [PHP Security Best Practices](https://www.php.net/manual/en/security.php)
