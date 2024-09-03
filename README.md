# API Testing with Postman

This guide will help you set up and test the API endpoints using Postman.

## Table of Contents

1. [Installation and Setup](#installation-and-setup)
2. [Environment Variables](#environment-variables)
3. [API Endpoints](#api-endpoints)
    - [Authentication](#authentication)
    - [User Management](#user-management)
    - [Posts](#posts)
    - [Comments](#comments)
4. [Running Tests](#running-tests)

## Installation and Setup

1. **Download and Install Postman:**  
   If you haven't installed Postman yet, you can download it from [Postman's official website](https://www.postman.com/downloads/).

2. **Import Collection:**  
   You can import a Postman collection by clicking on the "Import" button in Postman and uploading the collection file (`API_Postman_Collection.json`) provided in this repository.

## Environment Variables

Before running the tests, you'll need to set up the environment variables in Postman. Here's how to do it:

1. Click on the **gear icon** in the upper-right corner of Postman.
2. Click **Manage Environments**.
3. Add a new environment with the following variables:

    | Variable Name | Example Value               | Description                          |
    | ------------- | --------------------------- | ------------------------------------ |
    | `baseUrl`     | `http://localhost:5000/api/v1` | Base URL for the API                 |
    | `token`       | `Bearer your_jwt_token_here` | JWT token for authenticated requests |

## API Endpoints

### Authentication

- **Login User**
    - **Method:** POST
    - **URL:** `{{baseUrl}}/login`
    - **Body:** 
        ```json
        {
          "email": "user@example.com",
          "password": "password123"
        }
        ```
    - **Response:** JWT token and user data.

- **Register User**
    - **Method:** POST
    - **URL:** `{{baseUrl}}/register`
    - **Body:** 
        ```json
        {
          "name": "John Doe",
          "email": "john@example.com",
          "password": "password123",
          "avatar": "avatar_url_here"
        }
        ```
    - **Response:** JWT token and user data.

- **Logout User**
    - **Method:** GET
    - **URL:** `{{baseUrl}}/logout`
    - **Response:** Logout success message.

### User Management

- **Get Logged-In User**
    - **Method:** GET
    - **URL:** `{{baseUrl}}/me`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Response:** User data.

- **Update Profile**
    - **Method:** PUT
    - **URL:** `{{baseUrl}}/update/profile`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Body:** 
        ```json
        {
          "name": "John Updated",
          "email": "john.updated@example.com",
          "avatar": "new_avatar_url_here"
        }
        ```
    - **Response:** Success message.

- **Update Password**
    - **Method:** PUT
    - **URL:** `{{baseUrl}}/update/password`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Body:** 
        ```json
        {
          "oldPassword": "password123",
          "newPassword": "newpassword123"
        }
        ```
    - **Response:** Success message.

- **Forgot Password**
    - **Method:** POST
    - **URL:** `{{baseUrl}}/forgot/password`
    - **Body:** 
        ```json
        {
          "email": "user@example.com"
        }
        ```
    - **Response:** Success message.

- **Reset Password**
    - **Method:** PUT
    - **URL:** `{{baseUrl}}/password/reset/{{token}}`
    - **Body:** 
        ```json
        {
          "password": "newpassword123"
        }
        ```
    - **Response:** Success message.

### Posts

- **Get Posts of Following**
    - **Method:** GET
    - **URL:** `{{baseUrl}}/feed`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Response:** List of posts.

- **Get My Posts**
    - **Method:** GET
    - **URL:** `{{baseUrl}}/my/posts`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Response:** List of user's posts.

- **Create New Post**
    - **Method:** POST
    - **URL:** `{{baseUrl}}/post/upload`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Body:** 
        ```json
        {
          "caption": "My new post",
          "image": "image_url_here"
        }
        ```
    - **Response:** Success message.

- **Update Post**
    - **Method:** PUT
    - **URL:** `{{baseUrl}}/post/{{id}}`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Body:** 
        ```json
        {
          "caption": "Updated caption"
        }
        ```
    - **Response:** Success message.

- **Delete Post**
    - **Method:** DELETE
    - **URL:** `{{baseUrl}}/post/{{id}}`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Response:** Success message.

### Comments

- **Add Comment on Post**
    - **Method:** PUT
    - **URL:** `{{baseUrl}}/post/comment/{{id}}`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Body:** 
        ```json
        {
          "comment": "Nice post!"
        }
        ```
    - **Response:** Success message.

- **Delete Comment on Post**
    - **Method:** DELETE
    - **URL:** `{{baseUrl}}/post/comment/{{id}}`
    - **Headers:** 
        - `Authorization: {{token}}`
    - **Body:** 
        ```json
        {
          "commentId": "comment_id_here"
        }
        ```
    - **Response:** Success message.

## Running Tests

Once the environment is set up and the collection is imported, you can start testing each endpoint.

1. **Select the environment** from the top-right dropdown in Postman.
2. **Run the requests** individually by clicking the "Send" button.
3. **Check the response** to ensure the API is working as expected.

If you encounter any issues, verify that the environment variables are correctly set and that the API server is running.

---

Happy Testing!
