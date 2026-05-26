# 📦 Inventory Management System

A full-stack Inventory Management System built with **Java Spring Boot** (backend) and **HTML/CSS/JS + Bootstrap** (frontend), connected to a **MySQL** database.

---

## 🛠️ Tech Stack

| Layer      | Technology                          |
|------------|-------------------------------------|
| Backend    | Java 17, Spring Boot 3.2.5, Maven   |
| ORM        | Spring Data JPA + Hibernate         |
| Database   | MySQL 8.x                           |
| Frontend   | HTML5, CSS3, Bootstrap 5, Fetch API |

---

## 📁 Project Structure

```
inventory-management/
├── backend/                          # Spring Boot Maven project
│   ├── pom.xml
│   └── src/main/
│       ├── java/com/inventory/
│       │   ├── InventoryManagementApplication.java
│       │   ├── config/
│       │   │   └── CorsConfig.java
│       │   ├── controller/
│       │   │   └── ProductController.java
│       │   ├── model/
│       │   │   └── Product.java
│       │   ├── repository/
│       │   │   └── ProductRepository.java
│       │   └── service/
│       │       ├── ProductService.java
│       │       └── ProductServiceImpl.java
│       └── resources/
│           └── application.properties
├── frontend/
│   └── index.html                    # Single-page UI
├── database/
│   └── setup.sql                     # DB + table + sample data
└── README.md
```

---

## ⚙️ Prerequisites

Make sure you have the following installed:

- **Java 17+** → [Download](https://adoptium.net/)
- **Maven 3.8+** → [Download](https://maven.apache.org/download.cgi)
- **MySQL 8.x** → [Download](https://dev.mysql.com/downloads/)
- A web browser (Chrome, Firefox, Edge)

---

## 🚀 Setup & Running

### Step 1 — Set up the Database

1. Open MySQL Workbench or your MySQL CLI.
2. Run the SQL script:

```sql
SOURCE /path/to/inventory-management/database/setup.sql;
```

Or copy-paste the contents of `database/setup.sql` into your MySQL client.

This will:
- Create `inventory_db` database
- Create `products` table
- Insert 10 sample products

---

### Step 2 — Configure Database Credentials

Open `backend/src/main/resources/application.properties` and update:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/inventory_db?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true
spring.datasource.username=root       # ← your MySQL username
spring.datasource.password=root       # ← your MySQL password
```

---

### Step 3 — Start the Backend

```bash
cd backend
mvn spring-boot:run
```

The API will be running at: **http://localhost:8080**

You should see output like:
```
Started InventoryManagementApplication in 3.x seconds
```

---

### Step 4 — Open the Frontend

Simply open the file in your browser:

```
frontend/index.html
```

Double-click it or drag it into Chrome/Firefox — no server needed.

---

## 🔌 REST API Endpoints

| Method | Endpoint                  | Description              |
|--------|---------------------------|--------------------------|
| POST   | `/products`               | Add a new product        |
| GET    | `/products`               | Get all products         |
| GET    | `/products/{id}`          | Get product by ID        |
| PUT    | `/products/{id}`          | Update product by ID     |
| DELETE | `/products/{id}`          | Delete product by ID     |
| GET    | `/products/search?name=x` | Search products by name  |
| GET    | `/products/low-stock?threshold=10` | Low stock items |

### Example Request — Add Product

```bash
curl -X POST http://localhost:8080/products \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Laptop Pro 15",
    "quantity": 50,
    "price": 75000.00,
    "supplier": "Dell India"
  }'
```

### Example Response

```json
{
  "id": 1,
  "name": "Laptop Pro 15",
  "quantity": 50,
  "price": 75000.0,
  "supplier": "Dell India"
}
```

---

## 🖥️ Frontend Features

- **Dashboard stats** — Total products, total stock, inventory value, low-stock count
- **Add Product form** — Validate and submit new products
- **Products table** — View all products with color-coded stock badges
- **Edit** — Click Edit to pre-fill the form and update
- **Delete** — Confirm modal before deleting
- **Search** — Filter table by product name in real-time
- **Toast notifications** — Success/error feedback

---

## 🎨 Stock Badge Colors

| Badge Color | Meaning            |
|-------------|--------------------|
| 🟢 Green    | Quantity ≥ 10      |
| 🟡 Yellow   | Quantity 1–9 (Low) |
| 🔴 Red      | Out of stock (0)   |

---

## 🐞 Troubleshooting

| Problem | Solution |
|---------|----------|
| `Access denied for user 'root'` | Update MySQL credentials in `application.properties` |
| `Unknown database 'inventory_db'` | Run `database/setup.sql` first |
| Frontend shows "Cannot connect" | Make sure Spring Boot is running on port 8080 |
| Port 8080 already in use | Add `server.port=8081` to `application.properties` and update API URL in `index.html` |
| `java.sql.SQLSyntaxErrorException` | Verify MySQL version is 8.x and database exists |

---

## 📄 License

This project is open-source and free to use for educational and commercial purposes.
