# Chương trình học 4 buổi: Thiết kế Database cho hệ thống vừa và nhỏ

## Overview - Tổng quan chương trình

### 🎯 Mục tiêu tổng thể
Chương trình này được thiết kế để giúp học viên **thành thạo việc thiết kế cơ sở dữ liệu cho các hệ thống vừa và nhỏ**. Sau khi hoàn thành **4 buổi học (mỗi buổi 1 tiếng)**, học viên sẽ có khả năng:

- **Phân tích yêu cầu** và xác định các thực thể, mối quan hệ trong hệ thống
- **Thiết kế schema PostgreSQL** tuân thủ các nguyên tắc RDBMS và chuẩn hóa dữ liệu
- **Vẽ sơ đồ ERD** chuyên nghiệp để làm tài liệu database relationship
- **Áp dụng nguyên tắc thiết kế** SQL database hiệu quả cho PostgreSQL
- **Triển khai thực tế** với PostgreSQL và Prisma ORM trong stack Node.js/NestJS/Next.js

### 👥 Đối tượng người học
**Lập trình viên Full-stack** với profile sau:
- **Kinh nghiệm**: Tối thiểu 1 năm làm việc thực tế với web development
- **Tech Stack**: Node.js, NestJS, Next.js (JavaScript/TypeScript)  
- **Background**: Đã có kinh nghiệm cơ bản với SQL và database operations
- **Nhu cầu**: Muốn nâng cao kỹ năng thiết kế database chuyên nghiệp cho dự án thực tế

**Điều kiện tiên quyết:**
- ✅ Biết SQL cơ bản (SELECT, INSERT, UPDATE, DELETE, JOIN)
- ✅ Đã từng sử dụng PostgreSQL hoặc MySQL trong dự án
- ✅ Có kinh nghiệm với một ORM (TypeORM, Sequelize, Prisma...)
- ✅ Hiểu khái niệm cơ bản về REST API và backend development

### 🎁 Lợi ích cho người học
Sau khi hoàn thành khóa học, bạn sẽ:

#### 💼 Lợi ích nghề nghiệp
- **Tự tin thiết kế database** cho các dự án startup và SME
- **Tăng giá trị** như một full-stack developer với deep database knowledge
- **Giảm technical debt** trong các dự án hiện tại và tương lai
- **Communicate hiệu quả** với team về database architecture decisions

#### 🛠️ Kỹ năng thực tiễn
- **Làm chủ quy trình** thiết kế database từ requirements đến production
- **Tạo tài liệu ERD** chuyên nghiệp cho team và stakeholders  
- **Tối ưu performance** với indexing và query optimization strategies
- **Troubleshoot** các vấn đề database phổ biến trong production

#### 🚀 Impact dài hạn
- **Foundation vững chắc** cho việc học advanced topics (sharding, replication)
- **Mindset scalability** cho database architecture trong growth startups
- **Best practices** để maintain và scale database trong thực tế
- **Confidence** để lead technical discussions về database trong team

### Lộ trình học tập
```
Buổi 1: Nền tảng lý thuyết → Buổi 2: Thiết kế thực hành → Buổi 3: Tối ưu hiệu suất → Buổi 4: Triển khai công nghệ
```

### Công nghệ sử dụng
- **Database**: PostgreSQL (RDBMS chính)
- **ORM**: Prisma (Node.js/TypeScript)  
- **Framework**: NestJS (tùy chọn)
- **Công cụ thiết kế**: draw.io, Lucidchart, ERD Editor
- **Kiểm thử**: pgbench, JMeter, Artillery

### Dự án thực hành xuyên suốt
Chúng ta sẽ cùng xây dựng **hệ thống quản lý đơn hàng trực tuyến** từ khâu phân tích yêu cầu đến triển khai hoàn chỉnh, bao gồm các thực thể: Customer, Order, Product, OrderItem, Category.

---

## Buổi 1: Nền tảng thiết kế cơ sở dữ liệu quan hệ

📚 **Nội dung chi tiết:** [Lesson 1 - Nền tảng Thiết kế Database](./lesson-1.md)

### 🎯 Tóm tắt buổi học
- **Nắm vững tư duy thiết kế database** đúng đắn từ nguyên tắc đến thực hành  
- **Áp dụng 10 nguyên tắc vàng** trong thiết kế database cho dự án thực tế
- **Thực hiện quy trình 3 bước** để thiết kế database hiệu quả
- **Phát triển intuition** để đưa ra quyết định thiết kế hợp lý

### 🔑 Key Takeaways
- **Performance-First Design:** Thiết kế cho usage patterns thực tế
- **Strategic Normalization:** Chuẩn hóa đầu tiên, denormalize có mục đích  
- **Future-Proof Mindset:** Chuẩn bị cho scale và evolution
- **Quy trình 3 bước:** HIỂU → THIẾT KẾ → TỐI ƯU

---

## Buổi 2: Thiết kế lược đồ quan hệ & Sơ đồ ERD

### 🎯 Mục tiêu học tập
- **Phân tích yêu cầu** hệ thống để xác định thực thể và mối quan hệ
- **Thiết kế ERD** (Entity-Relationship Diagram) chuyên nghiệp
- Hiểu các **loại quan hệ**: 1-1, 1-n, n-n và cách triển khai
- Sử dụng **công cụ vẽ ERD** hiệu quả

### 📚 Quy trình thiết kế ERD

#### Bước 1: Phân tích yêu cầu và xác định thực thể
**Phương pháp:**
- Đọc kỹ yêu cầu, tìm các **danh từ quan trọng** → thực thể
- Tìm các **động từ mô tả hành động** → mối quan hệ
- Xác định **thuộc tính** cho mỗi thực thể

**Ví dụ với hệ thống đặt hàng:**
> "Khách hàng có thể đặt nhiều đơn hàng. Mỗi đơn hàng bao gồm nhiều sản phẩm với số lượng khác nhau. Sản phẩm được phân loại theo danh mục."

**Thực thể được xác định:**
- Customer (Khách hàng)
- Order (Đơn hàng)  
- Product (Sản phẩm)
- Category (Danh mục)
- OrderItem (Chi tiết đơn hàng - bảng trung gian)

#### Bước 2: Xác định các loại quan hệ

| Quan hệ | Ký hiệu | Ví dụ | Cách triển khai |
|---------|---------|-------|-----------------|
| **1-1** | -------- | User ↔ Profile | Khóa ngoại ở một bảng |
| **1-n** | ----<--- | Customer → Order | Khóa ngoại ở bảng "nhiều" |
| **n-n** | ----<>---- | Order ↔ Product | Bảng trung gian |

#### Bước 3: Vẽ sơ đồ ERD

**Quy ước ký hiệu:**
- **Hình chữ nhật**: Thực thể
- **Hình oval**: Thuộc tính
- **Hình thoi**: Mối quan hệ
- **Đường thẳng**: Kết nối các thành phần

### 💡 Ví dụ ERD hoàn chỉnh

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--o{ ORDER_ITEM : contains
    PRODUCT ||--o{ ORDER_ITEM : "appears in"
    CATEGORY ||--o{ PRODUCT : categorizes
    
    CUSTOMER {
        int id PK
        string name
        string email UK
        string phone
        timestamp created_at
    }
    
    ORDER {
        int id PK
        int customer_id FK
        timestamp order_date
        decimal total_amount
        string status
    }
    
    PRODUCT {
        int id PK
        string name
        decimal price
        int stock_quantity
        int category_id FK
        text description
    }
    
    CATEGORY {
        int id PK
        string name
        text description
    }
    
    ORDER_ITEM {
        int order_id FK
        int product_id FK
        int quantity
        decimal unit_price
    }
```

### 🛠️ Công cụ thiết kế ERD

#### Công cụ trực tuyến (miễn phí)
- **draw.io** (diagrams.net): Dễ sử dụng, nhiều template
- **Lucidchart**: Chuyên nghiệp, hỗ trợ cộng tác
- **dbdiagram.io**: Chuyên dụng cho database, syntax đơn giản

#### Extension VS Code
- **ERD Editor**: Vẽ ERD trực tiếp trong code
- **Database Client**: Kết nối và visualize database thực

#### Công cụ desktop
- **MySQL Workbench**: Miễn phí, mạnh mẽ
- **pgAdmin**: Chuyên dụng cho PostgreSQL

### 🛠️ Thực hành

#### Bài tập 1: Vẽ ERD cho hệ thống Blog
**Yêu cầu:**
- Người dùng có thể viết nhiều bài post
- Mỗi post thuộc một category 
- Người dùng có thể comment vào các post
- Post có thể có nhiều tag

**Deliverable:** File ERD hoàn chỉnh với đầy đủ thuộc tính và quan hệ

#### Bài tập 2: Review và cải thiện ERD
Cho ERD có sẵn, xác định các vấn đề:
- Thiếu thực thể quan trọng?
- Quan hệ có hợp lý?
- Thuộc tính có đặt đúng chỗ?

---

## Buổi 3: Tối ưu hiệu suất & Kiểm thử Database

### 🎯 Mục tiêu học tập
- **Đánh giá hiệu năng** database thông qua các chỉ số quan trọng
- **Áp dụng indexing** để tối ưu tốc độ truy vấn
- **Kiểm thử tải** với công cụ chuyên dụng
- **Cân bằng** giữa chuẩn hóa và hiệu suất (denormalization)

### 📚 Nguyên tắc tối ưu hiệu suất

#### 1. Chỉ số hiệu năng quan trọng
| Chỉ số | Ý nghĩa | Mục tiêu |
|--------|---------|----------|
| **QPS** (Queries Per Second) | Số truy vấn/giây | > 1000 QPS |
| **Response Time** | Thời gian đáp ứng | < 100ms (p95) |
| **Throughput** | Lượng dữ liệu xử lý | Tùy yêu cầu |
| **Error Rate** | Tỷ lệ lỗi | < 0.1% |
| **Resource Usage** | CPU, RAM, I/O | < 80% peak |

#### 2. Chiến lược Indexing

**Khi nào cần index:**
- Cột thường xuất hiện trong `WHERE`
- Cột dùng để `JOIN` giữa các bảng  
- Cột dùng trong `ORDER BY`
- Khóa ngoại (foreign key)

**Các loại index PostgreSQL:**
```sql
-- B-tree index (mặc định) - tốt cho equality và range queries
CREATE INDEX idx_customer_email ON customers (email);

-- Partial index - chỉ index một phần dữ liệu
CREATE INDEX idx_active_orders ON orders (customer_id) 
WHERE status = 'active';

-- Composite index - index trên nhiều cột
CREATE INDEX idx_order_date_status ON orders (order_date, status);

-- Unique index - đảm bảo tính duy nhất
CREATE UNIQUE INDEX idx_product_sku ON products (sku);
```

**Lưu ý về index:**
- ✅ Tăng tốc độ `SELECT`
- ❌ Làm chậm `INSERT/UPDATE/DELETE`
- ❌ Tốn thêm dung lượng lưu trữ

#### 3. Kỹ thuật Denormalization có kiểm soát

**Khi nào nên denormalize:**
- Hệ thống read-heavy (đọc nhiều hơn ghi)
- Join quá nhiều bảng gây chậm
- Cần tốc độ real-time

**Ví dụ denormalization:**
```sql
-- Thay vì join để lấy tên khách hàng mỗi lần
-- Có thể lưu thêm customer_name vào bảng orders
ALTER TABLE orders ADD COLUMN customer_name VARCHAR(100);

-- Cập nhật khi customer thay đổi tên (trade-off)
```

### 🔧 Công cụ kiểm thử và phân tích

#### 1. EXPLAIN ANALYZE - Công cụ tích hợp
```sql
-- Phân tích query plan
EXPLAIN ANALYZE 
SELECT o.*, c.name 
FROM orders o 
JOIN customers c ON o.customer_id = c.id 
WHERE o.order_date >= '2024-01-01';
```

**Đọc kết quả:**
- **Seq Scan**: Quét tuần tự (chậm) → cần index
- **Index Scan**: Sử dụng index (nhanh)
- **Nested Loop**: Join lồng nhau → kiểm tra điều kiện join
- **Cost**: Chi phí ước tính → so sánh các phương án

#### 2. pgbench - Benchmark tích hợp
```bash
# Khởi tạo dữ liệu test
pgbench -i -s 50 testdb

# Chạy test với 10 client, 100 transactions mỗi client
pgbench -c 10 -t 100 testdb
```

#### 3. JMeter - Kiểm thử tải toàn diện
**Thiết lập test plan:**
1. Thread Group: 100 users, ramp-up 60s
2. JDBC Connection Configuration
3. JDBC Request: Các query thường dùng
4. Listeners: View Results Tree, Summary Report

### 🛠️ Thực hành

#### Lab 1: Tối ưu Query Performance
**Bước 1:** Tạo dữ liệu test lớn
```sql
-- Chèn 100K customers
INSERT INTO customers (name, email) 
SELECT 
    'Customer ' || i,
    'user' || i || '@example.com'
FROM generate_series(1, 100000) i;

-- Chèn 1M orders
INSERT INTO orders (customer_id, order_date, total_amount)
SELECT 
    (random() * 99999 + 1)::int,
    '2023-01-01'::date + (random() * 365)::int,
    (random() * 1000 + 10)::numeric(10,2)
FROM generate_series(1, 1000000);
```

**Bước 2:** Đo thời gian query chậm
```sql
-- Query chậm: tìm tất cả đơn hàng của khách hàng theo email
SELECT o.* 
FROM orders o 
JOIN customers c ON o.customer_id = c.id 
WHERE c.email = 'user12345@example.com';
```

**Bước 3:** Thêm index và đo lại
```sql
CREATE INDEX idx_customers_email ON customers (email);
CREATE INDEX idx_orders_customer_id ON orders (customer_id);
```

**Kết quả mong đợi**: Thời gian giảm từ vài giây xuống < 10ms.

#### Lab 2: Load Testing với Artillery
```yaml
# artillery-config.yml
config:
  target: 'postgresql://user:pass@localhost:5432/testdb'
  phases:
    - duration: 60
      arrivalRate: 10
      name: "Warm up"
    - duration: 300  
      arrivalRate: 50
      name: "Peak load"

scenarios:
  - name: "Database queries"
    weight: 100
    engine: "postgres"
    queries:
      - "SELECT COUNT(*) FROM orders WHERE order_date >= CURRENT_DATE - INTERVAL '30 days'"
      - "SELECT c.name, SUM(o.total_amount) FROM customers c JOIN orders o ON c.id = o.customer_id GROUP BY c.id LIMIT 10"
```

```bash
# Chạy test
artillery run artillery-config.yml
```

---

## Buổi 4: Triển khai với Prisma ORM

### 🎯 Mục tiêu học tập
- **Thiết lập Prisma** trong dự án Node.js/TypeScript
- **Chuyển đổi ERD** thành Prisma schema
- **Quản lý migration** và phiên bản database
- **Tích hợp với NestJS** để xây dựng API hoàn chỉnh

### 📚 Giới thiệu Prisma ORM

#### Ưu điểm nổi bật
- ✅ **Type-safe**: Tích hợp chặt với TypeScript
- ✅ **Schema-first**: Định nghĩa model trước, generate code sau
- ✅ **Migration tự động**: Quản lý thay đổi database có phiên bản
- ✅ **Query builder trực quan**: Cú pháp dễ hiểu, mạnh mẽ
- ✅ **Prisma Studio**: GUI quản lý dữ liệu

#### Quy trình làm việc
```
Schema Definition → Migration → Code Generation → Application Code
```

### 🛠️ Thiết lập dự án

#### Bước 1: Khởi tạo dự án
```bash
# Tạo dự án mới
npm init -y
npm install prisma @prisma/client
npm install -D typescript @types/node ts-node

# Khởi tạo Prisma
npx prisma init
```

#### Bước 2: Cấu hình database
```env
# .env
DATABASE_URL="postgresql://username:password@localhost:5432/ecommerce"
```

#### Bước 3: Định nghĩa Prisma Schema
```prisma
// prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model Customer {
  id        Int      @id @default(autoincrement())
  name      String   @db.VarChar(100)
  email     String   @unique @db.VarChar(255)
  phone     String?  @db.VarChar(20)
  createdAt DateTime @default(now()) @map("created_at")
  
  // Relationships
  orders    Order[]
  
  @@map("customers")
}

model Category {
  id          Int     @id @default(autoincrement())
  name        String  @db.VarChar(100)
  description String?
  
  // Relationships  
  products    Product[]
  
  @@map("categories")
}

model Product {
  id            Int     @id @default(autoincrement())
  name          String  @db.VarChar(200)
  price         Decimal @db.Decimal(10, 2)
  stockQuantity Int     @default(0) @map("stock_quantity")
  description   String?
  categoryId    Int     @map("category_id")
  
  // Relationships
  category      Category    @relation(fields: [categoryId], references: [id])
  orderItems    OrderItem[]
  
  @@map("products")
}

   model Order {
     id          Int      @id @default(autoincrement())
  customerId  Int      @map("customer_id")
  orderDate   DateTime @default(now()) @map("order_date")
  totalAmount Decimal  @db.Decimal(10, 2) @map("total_amount")
  status      String   @default("pending") @db.VarChar(20)
  
  // Relationships
  customer    Customer    @relation(fields: [customerId], references: [id])
     orderItems  OrderItem[]
  
  @@map("orders")
}

   model OrderItem {
  orderId   Int     @map("order_id")
  productId Int     @map("product_id")
  quantity  Int
  unitPrice Decimal @db.Decimal(10, 2) @map("unit_price")
  
  // Relationships
     order     Order   @relation(fields: [orderId], references: [id])
     product   Product @relation(fields: [productId], references: [id])
  
  @@id([orderId, productId])
  @@map("order_items")
}
```

#### Bước 4: Chạy Migration
```bash
# Tạo và áp dụng migration đầu tiên
npx prisma migrate dev --name init

# Generate Prisma Client
npx prisma generate
```

### 💻 Sử dụng Prisma Client

#### CRUD cơ bản
```typescript
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

// CREATE - Tạo khách hàng mới
const newCustomer = await prisma.customer.create({
  data: {
    name: 'John Doe',
    email: 'john@example.com',
    phone: '+84123456789'
  }
})

// READ - Lấy danh sách đơn hàng kèm thông tin khách hàng
const ordersWithCustomers = await prisma.order.findMany({
  include: {
    customer: true,
    orderItems: {
      include: {
        product: true
      }
    }
  },
  where: {
    orderDate: {
      gte: new Date('2024-01-01')
    }
  },
  orderBy: {
    orderDate: 'desc'
  }
})

// UPDATE - Cập nhật trạng thái đơn hàng
const updatedOrder = await prisma.order.update({
  where: { id: 1 },
  data: { status: 'completed' }
})

// DELETE - Xóa sản phẩm
await prisma.product.delete({
  where: { id: 5 }
})
```

#### Query phức tạp
```typescript
// Thống kê doanh thu theo tháng
const monthlyRevenue = await prisma.order.groupBy({
  by: ['orderDate'],
  _sum: {
    totalAmount: true
  },
  where: {
    status: 'completed',
    orderDate: {
      gte: new Date('2024-01-01'),
      lt: new Date('2025-01-01')
    }
  }
})

// Transaction - Tạo đơn hàng với nhiều sản phẩm
const createOrderWithItems = await prisma.$transaction(async (tx) => {
  // Tạo đơn hàng
  const order = await tx.order.create({
    data: {
      customerId: 1,
      totalAmount: 299.99,
      status: 'pending'
    }
  })
  
  // Thêm sản phẩm vào đơn hàng
  await tx.orderItem.createMany({
    data: [
      {
        orderId: order.id,
        productId: 1,
        quantity: 2,
        unitPrice: 99.99
      },
      {
        orderId: order.id,
        productId: 2, 
        quantity: 1,
        unitPrice: 99.99
      }
    ]
  })
  
  return order
})
```

### 🏗️ Tích hợp với NestJS

#### Tạo PrismaService
```typescript
// src/prisma/prisma.service.ts
import { Injectable, OnModuleInit, OnModuleDestroy } from '@nestjs/common'
import { PrismaClient } from '@prisma/client'

@Injectable()
export class PrismaService extends PrismaClient implements OnModuleInit, OnModuleDestroy {
  async onModuleInit() {
    await this.$connect()
  }

  async onModuleDestroy() {
    await this.$disconnect()
  }
}
```

#### CustomerService với Prisma
```typescript
// src/customers/customers.service.ts
import { Injectable } from '@nestjs/common'
import { PrismaService } from '../prisma/prisma.service'
import { CreateCustomerDto, UpdateCustomerDto } from './dto'

@Injectable()
export class CustomersService {
  constructor(private prisma: PrismaService) {}

  async create(createCustomerDto: CreateCustomerDto) {
    return this.prisma.customer.create({
      data: createCustomerDto
    })
  }

  async findAll() {
    return this.prisma.customer.findMany({
      include: {
        orders: {
          include: {
            orderItems: {
              include: {
                product: true
              }
            }
          }
        }
      }
    })
  }

  async findOne(id: number) {
    return this.prisma.customer.findUnique({
      where: { id },
      include: {
        orders: true
      }
    })
  }

  async update(id: number, updateCustomerDto: UpdateCustomerDto) {
    return this.prisma.customer.update({
      where: { id },
      data: updateCustomerDto
    })
  }

  async remove(id: number) {
    return this.prisma.customer.delete({
      where: { id }
    })
  }
}
```

### 🛠️ Thực hành tổng hợp

#### Dự án: API Quản lý Đơn hàng
**Nhiệm vụ:** Xây dựng REST API hoàn chỉnh với các endpoint:

```
GET    /customers              # Danh sách khách hàng
POST   /customers              # Tạo khách hàng mới
GET    /customers/:id          # Thông tin khách hàng
PUT    /customers/:id          # Cập nhật khách hàng

GET    /products               # Danh sách sản phẩm
POST   /products               # Tạo sản phẩm mới
GET    /products/:id           # Thông tin sản phẩm

GET    /orders                 # Danh sách đơn hàng
POST   /orders                 # Tạo đơn hàng mới
GET    /orders/:id             # Chi tiết đơn hàng
PUT    /orders/:id/status      # Cập nhật trạng thái

GET    /analytics/revenue      # Báo cáo doanh thu
GET    /analytics/top-products # Sản phẩm bán chạy
```

#### Tính năng nâng cao
1. **Seed dữ liệu mẫu**
```typescript
// prisma/seed.ts
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

async function main() {
  // Tạo categories
  const electronics = await prisma.category.create({
    data: { name: 'Electronics', description: 'Electronic devices' }
  })
  
  // Tạo products
  await prisma.product.createMany({
    data: [
      {
        name: 'iPhone 15',
        price: 999.99,
        stockQuantity: 50,
        categoryId: electronics.id
      },
      {
        name: 'MacBook Pro',
        price: 2499.99,
        stockQuantity: 20,
        categoryId: electronics.id
      }
    ]
  })
}

main()
```

2. **Middleware logging**
```typescript
// src/prisma/prisma.service.ts
export class PrismaService extends PrismaClient implements OnModuleInit {
  constructor() {
    super({
      log: ['query', 'info', 'warn', 'error'],
    })
  }

  async onModuleInit() {
    // Log all queries for debugging
    this.$on('query', (e) => {
      console.log('Query: ' + e.query)
      console.log('Duration: ' + e.duration + 'ms')
    })
    
    await this.$connect()
  }
}
```

3. **Validation với class-validator**
```typescript
// src/customers/dto/create-customer.dto.ts
import { IsEmail, IsString, Length, IsOptional } from 'class-validator'

export class CreateCustomerDto {
  @IsString()
  @Length(2, 100)
  name: string

  @IsEmail()
  email: string

  @IsOptional()
  @IsString()
  @Length(10, 20)
  phone?: string
}
```

---

## 🎯 Kết luận và bước tiếp theo

### Tổng kết kiến thức đã học
Sau 4 buổi học, bạn đã nắm vững:

1. **Thiết kế database** theo nguyên tắc RDBMS và chuẩn hóa
2. **Phân tích yêu cầu** và vẽ sơ đồ ERD chuyên nghiệp
3. **Tối ưu hiệu suất** thông qua indexing và kiểm thử tải
4. **Triển khai thực tế** với Prisma ORM và NestJS

### Roadmap phát triển tiếp
- **Advanced Database**: Partitioning, Replication, Sharding
- **NoSQL Integration**: MongoDB, Redis caching
- **Database DevOps**: CI/CD cho migrations, backup strategies
- **Microservices**: Database per service, Event sourcing
- **Performance Monitoring**: APM tools, query optimization

### Tài liệu tham khảo
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Prisma Documentation](https://www.prisma.io/docs/)
- [Database Design Fundamentals](https://docs.microsoft.com/en-us/sql/relational-databases/database-design/)
- [NestJS Prisma Integration](https://docs.nestjs.com/recipes/prisma)

**Chúc mừng bạn đã hoàn thành chương trình! 🎉**
