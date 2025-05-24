# TableTalk API Documentation

## Overview
This API allows real-time communication for managing orders in a restaurant. It uses WebSocket for live updates on orders and HTTP for accessing and managing all system data including menus, products, orders, invoices, tables, maps, and user accounts.

# Index
- [Overview](#overview)
- [WebSocket Endpoints](#websocket-endpoints)
  - [Subscribe to Table Orders](#subscribe-to-table-orders)
  - [Update Table Order](#update-table-order)
  - [Subscribe to Kitchen Orders](#subscribe-to-kitchen-orders)
  - [Update Kitchen Orders](#update-kitchen-orders)
- [HTTP Endpoints](#http-endpoints)
  - [Menu Endpoints](#menu-endpoints)
  - [Product Endpoints](#product-endpoints)
  - [Category Endpoints](#category-endpoints)
  - [Order Endpoints](#order-endpoints)
  - [Invoice Endpoints](#invoice-endpoints)
  - [Table Endpoints](#table-endpoints)
  - [Map Endpoints](#map-endpoints)
  - [Print Endpoints](#print-endpoints)
  - [User Endpoints](#user-endpoints)
- [Models](#models)
  - [ProductDTO](#productdto)
  - [MenuItemDTO](#menuitemdto)
  - [CategoryDTO](#categorydto)
  - [MenuDTO](#menudto)
  - [OrderItemDTO](#orderitemdto)
  - [OrderDTO](#orderdto)
  - [TableDTO](#tabledto)
  - [TableMapDTO](#tablemapdto)
  - [MapDTO](#mapdto)
  - [InvoiceDTO](#invoicedto)
  - [UserDTO](#userdto)

## WebSocket Endpoints

### 1. Subscribe to Table Orders
- **Endpoint**: `/order/subscribe`
- **Method**: `POST` (WebSocket)
- **Description**: Subscribes the client to receive updates on a specific table's orders.
- **Request**: (body)
  ```json
  {
    "tableId": 1
  }
  ```
- **Response**: Upon subscribing, the current [OrderDTO](#orderdto) for the specified table will be sent back to the client.

### 2. Update Table Order
- **Endpoint**: /order
- **Method**: POST (WebSocket)
- **Description**: Updates the order for a specific table. All clients subscribed to the table will be notified of the updated order.
- **Request**: (body) [OrderDTO](#orderdto)
- **Response**: The updated [OrderDTO](#orderdto)

### 3. Subscribe to Kitchen Orders
- **Endpoint**: /kitchen/subscribe
- **Method**: POST (WebSocket)
- **Description**: Subscribes the client (typically the kitchen) to receive updates on all active orders.
- **Request**: (body) A list of [OrderDTO](#orderdto)
- **Response**: Upon subscribing, the current list of ongoing [OrderDTO](#orderdto) will be sent back to the client.

### 4. Update Kitchen Orders
- **Endpoint**: /kitchen
- **Method**: POST (WebSocket)
- **Description**: Allows the kitchen to update the status of all active orders. All clients subscribed to the kitchen's orders will receive the updated list.
- **Request**: (body) A list of [OrderDTO](#orderdto)
- **Response**: The updated list of [OrderDTO](#orderdto)

## HTTP Endpoints

### MENU
#### Get Available Menu
- **Endpoint**: `/menu/available`
- **Method**: `GET`
- **Description**: Retrieves the currently available menu with all its categories and items
- **Response**: [MenuDTO](#menudto)

### PRODUCTS
#### Get All Products
- **Endpoint**: `/products`
- **Method**: `GET`
- **Description**: Lists all products
- **Response**: Array of [ProductDTO](#productdto)

#### Create Product
- **Endpoint**: `/products`
- **Method**: `POST`
- **Description**: Creates a new product
- **Request**: [ProductDTO](#productdto)
- **Response**: [ProductDTO](#productdto)

#### Update Product
- **Endpoint**: `/products`
- **Method**: `PUT`
- **Description**: Updates an existing product
- **Request**: [ProductDTO](#productdto)
- **Response**: [ProductDTO](#productdto)

#### Delete Product
- **Endpoint**: `/products/{productId}`
- **Method**: `DELETE`
- **Description**: Deletes a product
- **Parameters**: productId (number)

### ORDERS
#### Get Orders by Filters
- **Endpoint**: `/orders/filters`
- **Method**: `GET`
- **Description**: Gets orders filtered by specified criteria
- **Query Parameters**:
  - orderId (number, optional): Filter by order ID
  - tableId (number, optional): Filter by table ID
  - status (string[], optional): Filter by order status (can specify multiple)
  - startDate (string, optional): Filter orders after this date (ISO format)
  - endDate (string, optional): Filter orders before this date (ISO format)
- **Response**: Array of [OrderDTO](#orderdto)

#### Create Empty Order for Table
- **Endpoint**: `/orders`
- **Method**: `POST`
- **Description**: Creates a new empty order for a specific table
- **Query Parameters**: tableId (number)
- **Response**: [OrderDTO](#orderdto)

#### Create Full Order
- **Endpoint**: `/orders/full`
- **Method**: `POST`
- **Description**: Creates a complete order with all its items
- **Request**: [OrderDTO](#orderdto)
- **Response**: [OrderDTO](#orderdto)

#### Update Order
- **Endpoint**: `/orders`
- **Method**: `PUT` 
- **Description**: Updates an existing order
- **Request**: [OrderDTO](#orderdto)
- **Response**: [OrderDTO](#orderdto)

#### Delete Order
- **Endpoint**: `/orders/{orderId}`
- **Method**: `DELETE`
- **Description**: Deletes an order
- **Parameters**: orderId (number)
- **Response**: void

### PRINT
#### Print Order
- **Endpoint**: `/print/order/{orderId}`
- **Method**: `GET`
- **Description**: Prints an order to a specific printer
- **Parameters**: 
  - orderId (number)
  - printer (string): The printer to use ('BAR' or 'KITCHEN')
- **Response**: [OrderDTO](#orderdto)

#### Print Invoice
- **Endpoint**: `/print/invoice/{invoiceId}`
- **Method**: `GET`
- **Description**: Prints an invoice to a specific printer
- **Parameters**: 
  - invoiceId (number)
  - printer (string): The printer to use ('BAR' or 'KITCHEN')
- **Response**: [InvoiceDTO](#invoicedto)

### INVOICES
#### Create Invoice
- **Endpoint**: `/invoice`
- **Method**: `POST`
- **Description**: Creates a new invoice
- **Request**: [InvoiceDTO](#invoicedto)
- **Response**: [InvoiceDTO](#invoicedto)

#### Get Invoices by Filters
- **Endpoint**: `/invoice/filters`
- **Method**: `GET`
- **Description**: Retrieves invoices based on filters
- **Query Parameters**:
  - invoiceId (number, optional): Filter by invoice ID
  - orderId (number, optional): Filter by order ID
  - tableNum (number, optional): Filter by table number
  - min (number, optional): Minimum total amount
  - max (number, optional): Maximum total amount
  - paymentType (string, optional): Type of payment
  - startDate (string, optional): Start date in ISO format
  - endDate (string, optional): End date in ISO format
- **Response**: Array of [InvoiceDTO](#invoicedto)

### TABLES
#### Get All Tables
- **Endpoint**: `/tables`
- **Method**: `GET`
- **Description**: Lists all tables
- **Response**: Array of [TableDTO](#tabledto)

#### Create Table
- **Endpoint**: `/tables`
- **Method**: `POST`
- **Description**: Creates a new table
- **Request**: [TableDTO](#tabledto)
- **Response**: [TableDTO](#tabledto)

#### Update Table
- **Endpoint**: `/tables`
- **Method**: `PUT`
- **Description**: Updates an existing table
- **Request**: [TableDTO](#tabledto)
- **Response**: [TableDTO](#tabledto)

#### Delete Table
- **Endpoint**: `/tables/{tableId}`
- **Method**: `DELETE`
- **Description**: Deletes a table
- **Parameters**: tableId (number)

### MAPS
#### Get All Maps
- **Endpoint**: `/map`
- **Method**: `GET`
- **Description**: Lists all maps
- **Response**: Array of [MapDTO](#mapdto)

#### Get Map by ID
- **Endpoint**: `/map/{mapId}`
- **Method**: `GET`
- **Description**: Gets a specific map
- **Parameters**: mapId (number)
- **Response**: [MapDTO](#mapdto)

#### Create Map
- **Endpoint**: `/map`
- **Method**: `POST`
- **Description**: Creates a new map
- **Query Parameters**: name (string)
- **Response**: [MapDTO](#mapdto)

#### Update Map
- **Endpoint**: `/map`
- **Method**: `PUT`
- **Description**: Updates an existing map
- **Request**: [MapDTO](#mapdto)
- **Response**: [MapDTO](#mapdto)

#### Delete Map
- **Endpoint**: `/map/{mapId}`
- **Method**: `DELETE`
- **Description**: Deletes a map
- **Parameters**: mapId (number)

### MENU CATEGORIES
#### Get All Categories
- **Endpoint**: `/menu-category`
- **Method**: `GET`
- **Description**: Lists all menu categories
- **Response**: Array of [CategoryDTO](#categorydto)

#### Create Category
- **Endpoint**: `/menu-category`
- **Method**: `POST`
- **Description**: Creates a new menu category
- **Request**: [CategoryDTO](#categorydto)
- **Response**: [CategoryDTO](#categorydto)

#### Update Category
- **Endpoint**: `/menu-category`
- **Method**: `PUT`
- **Description**: Updates an existing menu category
- **Request**: [CategoryDTO](#categorydto)
- **Response**: [CategoryDTO](#categorydto)

#### Delete Category
- **Endpoint**: `/menu-category/{categoryId}`
- **Method**: `DELETE`
- **Description**: Deletes a menu category
- **Parameters**: categoryId (number)

### USERS
#### Get All Users
- **Endpoint**: `/users`
- **Method**: `GET`
- **Description**: Lists all users
- **Response**: Array of [UserDTO](#userdto)

#### Get User by ID
- **Endpoint**: `/users/{id}`
- **Method**: `GET`
- **Description**: Gets a specific user
- **Parameters**: id (string)
- **Response**: [UserDTO](#userdto)

#### Create User
- **Endpoint**: `/users`
- **Method**: `POST`
- **Description**: Creates a new user
- **Query Parameters**: role (string): Role to assign to the user
- **Request**: [UserRegistrationDTO](#userregistrationdto)
- **Response**: [UserDTO](#userdto)

#### Update User
- **Endpoint**: `/users/{id}`
- **Method**: `PUT`
- **Description**: Updates an existing user
- **Parameters**: id (string)
- **Request**: [UserUpdateDTO](#userupdatedto)
- **Response**: [UserDTO](#userdto)

#### Delete User
- **Endpoint**: `/users/{id}`
- **Method**: `DELETE`
- **Description**: Deletes a user
- **Parameters**: id (string)

## Models

### ProductDTO
```json
{
  "id": 0,
  "name": "string",
  "description": "string",
  "url": "string",
  "stock": 0,
  "allergens": ["string"]
}
```

### MenuItemDTO
```json
{
  "id": 0,
  "price": 0,
  "tax": 0,
  "available": true,
  "product": {"$ref": "#ProductDTO"},
  "menuOrder": 0
}
```

### CategoryDTO
```json
{
  "id": 0,
  "name": "string",
  "description": "string",
  "menuItems": [{"$ref": "#MenuItemDTO"}],
  "menuOrder": 0
}
```

### MenuDTO
```json
{
  "id": 0,
  "name": "string",
  "description": "string",
  "available": true,
  "categories": [{"$ref": "#CategoryDTO"}]
}
```

### OrderItemDTO
```json
{
  "id": 0,
  "quantity": 0,
  "price": 0,
  "tax": 0,
  "note": "string",
  "status": "string",
  "menuItem": {"$ref": "#MenuItemDTO"},
  "completed": false
}
```

### OrderDTO
```json
{
  "id": 0,
  "totalWithoutTax": 0,
  "totalWithTax": 0,
  "date": "2024-04-21T12:00:00Z",
  "status": "PENDING",
  "orderItems": [{"$ref": "#OrderItemDTO"}],
  "table": {"$ref": "#TableDTO"},
  "paid": false
}
```

### TableDTO
```json
{
  "id": 0,
  "number": 0,
  "capacity": 0,
  "location": "string" // ENUM: BAR_AREA, INDOOR_SEATING, OUTDOOR_SEATING
}
```

### TableMapDTO
```json
{
  "table": {"$ref": "#TableDTO"},
  "x": 0,
  "y": 0,
  "width": 0,
  "height": 0,
  "angle": 0
}
```

### MapDTO
```json
{
  "id": 0,
  "name": "string",
  "tableMap": [{"$ref": "#TableMapDTO"}]
}
```

### InvoiceDTO
```json
{
  "id": 0,
  "date": "2024-04-21T12:00:00Z",
  "paidWithCard": 0,
  "paidWithCash": 0,
  "order": {"$ref": "#OrderDTO"},
  "customer_name": "string",
  "customer_id": "string",
  "address": "string"
}
```

### UserDTO
```json
{
  "id": "string",
  "username": "string",
  "email": "string",
  "firstName": "string",
  "lastName": "string",
  "role": "string", // ENUM: ADMIN, MANAGER, WORKER
  "enabled": true,
  "createdAt": "2024-04-21T12:00:00Z",
  "updatedAt": "2024-04-21T12:00:00Z"
}
```

### UserRegistrationDTO
```json
{
  "username": "string",
  "email": "string",
  "password": "string",
  "firstName": "string",
  "lastName": "string"
}
```

### UserUpdateDTO
```json
{
  "username": "string",
  "email": "string",
  "password": "string",
  "firstName": "string",
  "lastName": "string",
  "role": "string", // ENUM: ADMIN, MANAGER, WORKER
  "enabled": true
}
```