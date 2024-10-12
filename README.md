
# TeleBook Contacts API

This API allows you to manage contacts and mark them as favorites in the TeleBook application. The backend is built using Flask and uses MySQL as the database.

## Requirements

- Python 3.x
- Flask
- Flask-MySQLdb
- MySQL

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/your-repo/telebook-api.git
    cd telebook-api
    ```

2. Install dependencies:
    ```bash
    pip install Flask Flask-MySQLdb flask-cors
    ```

3. Set up your MySQL database:
    ```sql
    CREATE DATABASE contactsDB;
    
    USE contactsDB;

    CREATE TABLE contacts (
        id INT AUTO_INCREMENT PRIMARY KEY,
        firstName VARCHAR(100),
        lastName VARCHAR(100),
        phone VARCHAR(15),
        email VARCHAR(100)
    );

    CREATE TABLE favorites (
        id INT AUTO_INCREMENT PRIMARY KEY,
        contact_id INT,
        FOREIGN KEY (contact_id) REFERENCES contacts(id) ON DELETE CASCADE
    );
    ```

4. Configure MySQL credentials in `app.py`:
    ```python
    app.config['MYSQL_HOST'] = 'localhost'
    app.config['MYSQL_USER'] = 'your_mysql_user'
    app.config['MYSQL_PASSWORD'] = 'your_mysql_password'
    app.config['MYSQL_DB'] = 'contactsDB'
    ```

5. Run the Flask app:
    ```bash
    python app.py
    ```

The server will be running on `http://127.0.0.1:5000`.

## API Endpoints

### 1. **Get All Contacts**

- **Endpoint**: `/contacts`
- **Method**: `GET`
- **Description**: Retrieves all contacts.
- **Response**:
  ```json
  [
    {
      "id": 1,
      "firstName": "Alice",
      "lastName": "Smith",
      "phone": "9876543210",
      "email": "alice.smith@example.com"
    },
    {
      "id": 2,
      "firstName": "Bob",
      "lastName": "Johnson",
      "phone": "1234567890",
      "email": "bob.johnson@example.com"
    }
  ]
  ```

### 2. **Add a Contact**

- **Endpoint**: `/contacts`
- **Method**: `POST`
- **Description**: Adds a new contact.
- **Request Body**:
  ```json
  {
    "firstName": "George ",
    "lastName": "Bush",
    "phone": "123456789",
    "email": "bush.George@example.com"
  }
  ```
- **Response**:
  ```json
  {
    "msg": "Contact added successfully"
  }
  ```

### 3. **Update a Contact**

- **Endpoint**: `/contacts/<id>`
- **Method**: `PUT`
- **Description**: Updates an existing contact by ID.
- **Request Body**:
  ```json
  {
    "firstName": "George",
    "lastName": "Bush",
    "phone": "9876543210",
    "email": "bush.newemail@example.com"
  }
  ```
- **Response**:
  ```json
  {
    "msg": "Contact updated successfully"
  }
  ```

### 4. **Delete a Contact**

- **Endpoint**: `/contacts/<id>`
- **Method**: `DELETE`
- **Description**: Deletes a contact by ID.
- **Response**:
  ```json
  {
    "msg": "Contact deleted successfully"
  }
  ```

### 5. **Add Contact to Favorites**

- **Endpoint**: `/favorites/<contact_id>`
- **Method**: `POST`
- **Description**: Adds a contact to the favorites list.
- **Response**:
  ```json
  {
    "msg": "Contact added to favorites"
  }
  ```

### 6. **Get All Favorite Contacts**

- **Endpoint**: `/favorites`
- **Method**: `GET`
- **Description**: Retrieves all favorite contacts.
- **Response**:
  ```json
  [
    {
      "id": 1,
      "firstName": "Alice",
      "lastName": "Smith",
      "phone": "9876543210",
      "email": "alice.smith@example.com"
    },
    {
      "id": 3,
      "firstName": "John",
      "lastName": "Doe",
      "phone": "123456789",
      "email": "john.doe@example.com"
    }
  ]
  ```

### 7. **Remove Contact from Favorites**

- **Endpoint**: `/favorites/<contact_id>`
- **Method**: `DELETE`
- **Description**: Removes a contact from the favorites list by `contact_id`.
- **Response**:
  ```json
  {
    "msg": "Contact removed from favorites"
  }
  ```
