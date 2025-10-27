# 🏗️ EProject Phase 1 – Microservices Architecture

Dự án mô phỏng hệ thống Microservices gồm các dịch vụ:  
API Gateway, Auth Service, Product Service và Order Service, giao tiếp qua RabbitMQ và lưu trữ dữ liệu trên MongoDB.

--------------------------------------------------------------------------------
📂 CẤU TRÚC THƯ MỤC
--------------------------------------------------------------------------------
```bash
EProject-Phase-1/
│
├── api-gateway/
│   ├── index.js
│   ├── package.json
│   └── package-lock.json
│
├── auth/
│   ├── src/
│   │   ├── app.js
│   │   ├── config/index.js
│   │   ├── controllers/authControllers.js
│   │   ├── middlewares/authMiddleware.js
│   │   ├── models/user.js
│   │   ├── repositories/userRepository.js
│   │   ├── services/authService.js
│   │   └── test/authController.test.js
│   ├── index.js
│   ├── package.json
│   └── package-lock.json
│
├── order/
│   ├── src/
│   │   ├── app.js
│   │   ├── config.js
│   │   ├── models/order.js
│   │   └── utils/
│   │       ├── isAuthenticated.js
│   │       └── messageBroker.js
│   ├── index.js
│   ├── package.json
│   └── package-lock.json
│
├── product/
│   ├── src/
│   │   ├── app.js
│   │   ├── config.js
│   │   ├── controllers/productControllers.js
│   │   ├── models/product.js
│   │   ├── repositories/productRepository.js
│   │   ├── routes/productRoutes.js
│   │   ├── services/productsService.js
│   │   ├── test/product.test.js
│   │   └── utils/
│   │       ├── isAuthenticated.js
│   │       └── messageBroker.js
│   ├── index.js
│   ├── package.json
│   └── package-lock.json
│
├── utils/
│   └── isAuthenticated.js
│
├── .gitignore
├── docker-compose.yml
├── package.json
├── package-lock.json
└── README.md
```

--------------------------------------------------------------------------------
⚙️ CÔNG NGHỆ SỬ DỤNG
--------------------------------------------------------------------------------
Backend Framework : Node.js + Express  
Database : MongoDB  
Message Queue : RabbitMQ  
Authentication : JWT  
Containerization : Docker & Docker Compose

--------------------------------------------------------------------------------
🚀 CÁCH CHẠY HỆ THỐNG
--------------------------------------------------------------------------------
# 1️⃣ Tắt tất cả container cũ
docker-compose down -v

# 2️⃣ Build lại toàn bộ dịch vụ
docker-compose up --build -d

# 3️⃣ Khởi động container
docker-compose up -d

# 4️⃣ (Tuỳ chọn) Build hoặc start riêng từng service
docker-compose build product
docker-compose up product

--------------------------------------------------------------------------------
🌐 API ENDPOINTS
--------------------------------------------------------------------------------
# 1. AUTH SERVICE
## Đăng ký
POST http://localhost:3003/auth/register
{
  "username": "quynhnhu",
  "password": "123"
}

## Đăng nhập
POST http://localhost:3003/auth/login
{
  "username": "quynhnhu",
  "password": "123"
}

## Dashboard (kiểm tra JWT)
GET http://localhost:3003/auth/dashboard

--------------------------------------------------------------------------------
# 2. PRODUCT SERVICE
## Tạo sản phẩm
POST http://localhost:3003/products/api/products
Header:
Authorization: Bearer <token>
Body:
{
  "name": "Laptop",
  "price": 50000,
  "description": "Laptop ASUS Gaming TUF F16"
}

## Lấy danh sách sản phẩm
GET http://localhost:3003/products/api/products

## Lấy chi tiết sản phẩm
GET http://localhost:3003/products/api/products/<productId>

--------------------------------------------------------------------------------
# 3. ORDER SERVICE
## Tạo đơn hàng
POST http://localhost:3003/products/api/products/buy
{
  "ids": [
    "68f5a78837a2cf0201fa92eb"
  ]
}

--------------------------------------------------------------------------------
🧩 API GATEWAY
--------------------------------------------------------------------------------
API Gateway định tuyến:
- /auth/*  → Auth Service
- /products/* → Product Service
- /orders/* → Order Service

--------------------------------------------------------------------------------
🧠 GHI CHÚ QUAN TRỌNG
--------------------------------------------------------------------------------
Port mặc định:
| Service      | Port nội bộ | Map ra ngoài |
|---------------|-------------|---------------|
| API Gateway   | 3003        | 3003          |
| Auth          | 3000        | -             |
| Product       | 3001        | -             |
| Order         | 3002        | -             |
| MongoDB       | 27017       | 27017         |
| RabbitMQ      | 5672 / 15672| 5672 / 15672  |

Tất cả request đi qua API Gateway: http://localhost:3003  
Xem log service:
docker logs <container_name>

--------------------------------------------------------------------------------
🧾 GIT COMMANDS
--------------------------------------------------------------------------------
git add .
git commit -m "chore: push full project structure"
git push origin main

--------------------------------------------------------------------------------
✅ KẾT QUẢ MONG ĐỢI
--------------------------------------------------------------------------------
- API Gateway sẵn sàng tại http://localhost:3003  
- Auth, Product, Order hoạt động độc lập  
- RabbitMQ giao tiếp qua queue "orders" và "products"  
- MongoDB lưu user, product, order

--------------------------------------------------------------------------------
🧰 TÁC GIẢ
--------------------------------------------------------------------------------
Nguyễn Thị Quỳnh Như - 22663381
EProject Phase 1 – Node.js Microservices (2025)
