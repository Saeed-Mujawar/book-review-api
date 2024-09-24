# Book Review API

This API is built with FastAPI and offers a platform for users to manage books, reviews, and tags. It includes robust features like JWT authentication, background task processing with Celery, database interaction using SQLModel, and more.

## Features
- User authentication and authorization with JWT.
- CRUD operations for books, reviews, and tags.
- Email support for account verification and password resets.
- Asynchronous processing of background tasks using Celery.
- Database interactions with SQLModel and Alembic for migrations.
- Role-based access control.
- Comprehensive API documentation via Swagger and Redoc.
- Deployed on Render.com.

## Core Concepts

### 1. REST API and Routing
- **Build a REST API on a Python List:** Initially implemented basic CRUD operations using a Python list before transitioning to a database.
- **Organizing API Paths with Routers:** Split API logic into different routers for modular code and scalability.

### 2. Database Integration
- **Databases With SQLModel:** Utilized SQLModel to define database schemas, interact with the database asynchronously, and handle relationships.
- **Setting Up a Database:** Set up a PostgreSQL database and integrated it into the FastAPI application.
- **Async SQLModel Setup:** Managed asynchronous connections to the database using SQLModel.
- **Database Connection with Lifespan Events:** Handled database connections and cleanup during the app’s lifespan.

### 3. CRUD Logic and Dependency Injection
- **Creating Database Tables:** Automatically generated database tables from SQLModel models.
- **Separate CRUD Logic Using Service Classes:** Split CRUD operations into service classes to keep the code clean and reusable.
- **Intro to Dependency Injection:** Applied FastAPI's Dependency Injection to manage services and database sessions.
- **Use Service Methods in API Handlers:** Connected the API path handlers with service methods for performing CRUD operations.

### 4. Authentication & Authorization
- **User Auth Model:** Created a user model for authentication, integrated with FastAPI.
- **JWT Authentication:** Utilized PyJWT for token-based authentication and implemented endpoints for login and account creation.
- **Password Hashing with Passlib:** Secured user passwords using `passlib` for hashing.
- **Role-Based Access Control:** Added roles to users and created role-checking dependencies to restrict access based on roles.

### 5. Email and Account Verification
- **Email Support:** Set up FastAPI-Mail to handle email notifications for account verification and password resets.
- **User Account Verification:** Sent verification emails and implemented token-based account activation.

### 6. Background Tasks
- **Background Tasks with Celery and Redis:** Offloaded heavy tasks, like sending emails, to background workers using Celery and Redis.
- **Celery Monitoring with Flower:** Monitored and managed background tasks via Flower.

### 7. Error Handling and Middleware
- **Error Handling:** Created custom API exceptions and registered handlers for managing different types of errors.
- **Middleware:** Integrated custom middleware for logging and added CORS and Trusted Hosts middleware for enhanced security.

### 8. API Documentation
- **Swagger and Redoc:** Automatically generated and served interactive API documentation using SwaggerUI and Redoc.

### 9. Deployment
- **Deployment on Render.com:** Deployed the FastAPI app on Render.com for scalable and free hosting.


---

## API Endpoints

### Books

Manage books with the following endpoints:

- **GET /api/v1/books/**  
  Retrieve all books in the system.

- **POST /api/v1/books/**  
  Create a new book entry.  
  **Request Body Example:**
  ```json
  {
    "title": "Book Title",
    "author": "Author Name",
    "publisher": "Publisher Name",
    "published_date": "2023-01-01",
    "page_count": 350,
    "language": "English"
  }

- **GET /api/v1/books/user/{user_uid}**  
  Retrieves all book submissions by a specific user.

- **GET /api/v1/books/{book_uid}**  
  Retrieves a single book by its unique identifier.


- **PATCH /api/v1/books/{book_uid}**  
  Updates the details of a book. You can update any of the fields like title, author, or publisher.

  **Request Body Example:**
  ```json
  {
    "title": "Updated Book Title",
    "publisher": "Updated Publisher Name"
  }

- **DELETE /api/v1/books/{book_uid}**  
  Deletes a book from the system.

---

### Authentication

The API provides user authentication features including signup, login, and token-based session management.

- **POST /api/v1/auth/send_mail**  
  Sends a verification email to the user for account confirmation.

- **POST /api/v1/auth/signup**  
  Registers a new user in the system.
  **Request Body Example:**
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword123"
  }

- **GET /api/v1/auth/verify/{token}**  
  Verifies the user account using the token sent to their email.

- **POST /api/v1/auth/login**  
  Authenticates the user and returns a JSON Web Token (JWT) for subsequent authenticated requests.

  **Request Body Example:**
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword123"
  }

- **GET /api/v1/auth/refresh_token**  
  Generates a new access token using a refresh token.

- **GET /api/v1/auth/me**  
Retrieves the current authenticated user's details.
- **GET /api/v1/auth/logout**  
  Retrieves the current authenticated user's details.
- **POST /api/v1/auth/password-reset-request**  
Requests a password reset link via email.

- **POST /api/v1/auth/password-reset-confirm/{token}**  
Resets the user's password after verifying the token.

---

### Reviews

These endpoints manage reviews associated with books:

- **GET /api/v1/reviews/**  
  Get a list of all reviews.

- **GET /api/v1/reviews/{review_uid}**  
  Retrieve the details of a specific review.

- **DELETE /api/v1/reviews/{review_uid}**  
  Delete a review.

- **POST /api/v1/reviews/book/{book_uid}**  
  Add a review to a specific book.

    **Request Body Example:**
  ```json
  {
    "review_text": "Great book, highly recommend!",
    "rating": 5
  }

---

### Tags

These endpoints manage tags for categorizing books:

- **GET /api/v1/tags/**  
  Get a list of all tags.

- **POST /api/v1/tags/**  
  Create a new tag.

    **Request Body Example:**
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword123"
  }

- **POST /api/v1/tags/book/{book_uid}/tags**  
  Add tags to a specific book.
    **Request Body Example:**
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword123"
  }

- **PUT /api/v1/tags/{tag_uid}**  
  Update an existing tag.
    **Request Body Example:**
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword123"
  }

- **DELETE /api/v1/tags/{tag_uid}**  
  Delete a tag.

---

  ## Summary

The Book Review API provides a robust platform for users to manage books, reviews, and tags while ensuring secure user authentication and authorization.

---

## Requirements

- **Python 3.7+**

- **FastAPI**

- **PostgreSQL**

## Installation
To set up the Book Review API, follow these steps:

1. **Clone the repository:**

   ```bash
   git clone https://github.com/your-username/book-review-api.git
   cd book-review-api

2. **Create and activate a virtual environment:**

   ```bash
   python -m venv env
source env/bin/activate   # On Windows: env\Scripts\activate

3. **Install the required dependencies:**

   ```bash
pip install -r requirements.txt
4. **Set up the environment variables:**

   Create a .env file in the root directory of the project and add the necessary environment variables.

5. **Run the database migrations:**

   ```bash
   alembic upgrade head

6. **Start the FastAPI server:**

   ```bash
   fastapi dev src/  
