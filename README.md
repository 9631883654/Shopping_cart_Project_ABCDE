# Shopping Cart Project

A full-stack e-commerce shopping cart application built with Go (Gin, GORM) backend and React frontend.

## Project Structure

```
Shopping_cart_Project_ABCDE/
├── backend/          # Go backend API
│   ├── models/       # Database models
│   ├── handlers/     # API handlers
│   ├── middleware/   # Authentication middleware
│   ├── database/     # Database setup
│   └── main.go       # Application entry point
├── frontend/         # React frontend
│   ├── src/
│   │   ├── components/  # React components
│   │   └── services/    # API service layer
│   └── public/
└── README.md
```

## Features

- User registration and authentication
- Item management (create and list items)
- Shopping cart functionality
- Order placement and history
- Single device login (one token per user)

## Prerequisites

- Go 1.21 or higher
- Node.js 16+ and npm
- SQLite (included with GORM)

## Quick Start

1. **Start the backend:**
   ```bash
   cd backend
   go mod download
   go run scripts/seed_data.go  # Optional: Add sample items
   go run main.go
   ```

2. **Start the frontend (in a new terminal):**
   ```bash
   cd frontend
   npm install
   npm start
   ```

3. **Access the application:**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8080

4. **Create a user account:**
   - Use Postman collection to create a user via `POST /users`
   - Or use the API directly

## Backend Setup

1. Navigate to the backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
go mod download
```

3. (Optional) Seed sample data:
```bash
go run scripts/seed_data.go
```

4. Run the server:
```bash
go run main.go
```

The backend server will start on `http://localhost:8080`

## Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm start
```

The frontend will start on `http://localhost:3000`

## API Endpoints

### Public Endpoints

- `POST /users` - Create a new user
  ```json
  {
    "username": "john_doe",
    "password": "password123"
  }
  ```

- `GET /users` - List all users

- `POST /users/login` - Login user
  ```json
  {
    "username": "john_doe",
    "password": "password123"
  }
  ```
  Returns: `{ "token": "...", "user_id": 1 }`

- `POST /items` - Create a new item
  ```json
  {
    "name": "Laptop",
    "description": "High performance laptop",
    "price": 999.99
  }
  ```

- `GET /items` - List all items

### Protected Endpoints (Require Authorization Header: `Bearer <token>`)

- `POST /carts` - Create/update cart with items
  ```json
  {
    "item_ids": [1, 2, 3]
  }
  ```

- `GET /carts` - List all carts (admin)

- `GET /carts/user` - Get current user's cart

- `POST /orders` - Create order from cart
  ```json
  {
    "cart_id": 1
  }
  ```

- `GET /orders` - List all orders (admin)

- `GET /orders/user` - Get current user's orders

## Frontend Usage

1. **Login Screen**: Enter username and password to login. If you don't have an account, you can create one using the API or Postman collection.

2. **Items List Screen**: 
   - View all available items
   - Click on any item to add it to your cart
   - Use the **Cart** button to view your cart items
   - Use the **Order History** button to view your past orders
   - Use the **Checkout** button to convert your cart to an order

## Testing with Postman

Import the `Shopping_Cart_API.postman_collection.json` file into Postman to test all API endpoints.

### Steps to test:

1. Create a user: `POST /users`
2. Login: `POST /users/login` (copy the token from response)
3. Create items: `POST /items` (add Authorization header with token)
4. Add items to cart: `POST /carts` (add Authorization header with token)
5. Create order: `POST /orders` (add Authorization header with token)

## Database

The application uses SQLite database (`shopping_cart.db`) which is automatically created in the backend directory when you first run the application.

## Notes

- A user can only be logged in from a single device at a time (new login replaces the previous token)
- Each user can have only one cart
- When an order is created, the cart is cleared
- Inventory management is not implemented (no stock tracking)

## Technologies Used

### Backend
- Go 1.21
- Gin Web Framework
- GORM ORM
- SQLite Database
- JWT-style token authentication

### Frontend
- React 18
- React Router
- Axios
- React Toastify

## License

This project is created for demonstration purposes.

