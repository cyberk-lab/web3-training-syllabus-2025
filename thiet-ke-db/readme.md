# Chương trình học 4 buổi: Thiết kế Database cho hệ thống vừa và nhỏ

## Overview - Tổng quan chương trình

### Mục tiêu tổng thể
Chương trình này được thiết kế để giúp học viên **thành thạo việc thiết kế cơ sở dữ liệu** cho các hệ thống quy mô vừa và nhỏ. Sau khi hoàn thành, học viên sẽ có khả năng:

- 🎯 **Phân tích yêu cầu** và xác định các thực thể, mối quan hệ trong hệ thống
- 🏗️ **Thiết kế schema** tuân thủ các nguyên tắc RDBMS và chuẩn hóa dữ liệu
- 📊 **Vẽ sơ đồ ERD** chuyên nghiệp để trình bày thiết kế
- ⚡ **Tối ưu hiệu suất** database thông qua indexing và kiểm thử tải
- 🔧 **Triển khai thực tế** với PostgreSQL và Prisma ORM trong môi trường Node.js/NestJS

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

### 🎯 Mục tiêu học tập
- Hiểu sâu các **nguyên tắc cốt lõi** của cơ sở dữ liệu quan hệ (RDBMS)
- Nắm vững cách sử dụng **khóa chính** và **khóa ngoại** để tạo mối liên kết
- Áp dụng **chuẩn hóa dữ liệu** (1NF, 2NF, 3NF) để tránh dư thừa
- Chọn **kiểu dữ liệu** và **ràng buộc** phù hợp cho PostgreSQL

### 📋 Các nguyên tắc thiết kế database

Trước khi đi vào chi tiết kỹ thuật, hãy nắm vững **10 nguyên tắc vàng** trong thiết kế database:

#### 1. 🚀 Nguyên tắc tối ưu hiệu suất (Performance-First Design)
- **Thiết kế cho tốc độ query**: Ưu tiên các truy vấn thường dùng nhất
- **Read-heavy optimization**: Tối ưu cho việc đọc dữ liệu (80% workload thường là SELECT)
- **Minimize JOIN operations**: Giảm thiểu số lượng bảng cần join trong query quan trọng
- **Consider query patterns**: Phân tích các pattern truy vấn trước khi thiết kế schema

#### 2. 📊 Nguyên tắc chuẩn hóa có chọn lọc
- **Start normalized**: Bắt đầu với thiết kế chuẩn hóa hoàn toàn
- **Denormalize strategically**: Chỉ phi chuẩn hóa khi có lý do cụ thể về hiệu suất
- **Document trade-offs**: Ghi chép lại lý do denormalization để maintain sau này
- **Balance consistency vs speed**: Cân bằng giữa tính nhất quán và tốc độ

#### 3. 🎯 Nguyên tắc thiết kế hướng tương lai (Future-Proof Design)
- **Scalability mindset**: Thiết kế để có thể scale (horizontal/vertical)
- **Extension friendly**: Dễ dàng thêm field, bảng mới mà không phá vỡ cấu trúc
- **Version-aware**: Chuẩn bị cho việc migration và schema evolution
- **Partition consideration**: Dự đoán nhu cầu phân vùng dữ liệu trong tương lai

#### 4. 🔒 Nguyên tắc bảo mật và toàn vẹn dữ liệu
- **Data integrity first**: Constraints, foreign keys để đảm bảo dữ liệu đúng
- **Principle of least privilege**: Chỉ cấp quyền tối thiểu cần thiết
- **Audit trail**: Thiết kế sẵn việc theo dõi thay đổi dữ liệu quan trọng
- **Sensitive data handling**: Riêng biệt dữ liệu nhạy cảm (PII, payment info)

#### 5. 🛠️ Nguyên tắc dễ bảo trì (Maintainability)
- **Clear naming conventions**: Tên bảng, cột rõ ràng, nhất quán
- **Self-documenting schema**: Thiết kế tự giải thích được mục đích
- **Consistent patterns**: Sử dụng pattern nhất quán trong toàn bộ database
- **Change management**: Có quy trình rõ ràng cho việc thay đổi schema

#### 6. 💾 Nguyên tắc tối ưu lưu trữ
- **Right-size data types**: Chọn kiểu dữ liệu vừa đủ, không lãng phí
- **Storage efficiency**: Cân nhắc compression, partitioning cho bảng lớn
- **Archive strategy**: Lên kế hoạch cho dữ liệu cũ (archive vs delete)
- **Index strategy**: Index đúng chỗ, tránh over-indexing

#### 7. 🔄 Nguyên tắc transaction và consistency
- **ACID compliance**: Đảm bảo tính atomicity, consistency, isolation, durability
- **Transaction boundaries**: Thiết kế transaction scope hợp lý
- **Deadlock prevention**: Tránh thiết kế gây deadlock
- **Concurrency handling**: Chuẩn bị cho multi-user access

#### 8. 📈 Nguyên tắc monitoring và observability
- **Query performance tracking**: Thiết kế để có thể monitor query performance
- **Usage analytics**: Chuẩn bị metadata để phân tích usage pattern
- **Error handling**: Thiết kế error states và logging
- **Health checks**: Các query đơn giản để check database health

#### 9. 🔧 Nguyên tắc phù hợp với ứng dụng
- **Application-driven design**: Thiết kế theo nhu cầu thực tế của ứng dụng
- **API-friendly**: Cấu trúc dữ liệu phù hợp với API endpoints
- **Caching consideration**: Thiết kế tương thích với caching strategies
- **Development workflow**: Phù hợp với quy trình phát triển của team

#### 10. 🌍 Nguyên tắc đa môi trường
- **Environment consistency**: Schema nhất quán giữa dev, staging, production
- **Deployment strategy**: Chuẩn bị cho zero-downtime deployment
- **Backup and recovery**: Thiết kế recovery-friendly
- **Cross-region consideration**: Chuẩn bị cho distributed deployment

### ⚖️ Thứ tự ưu tiên trong thiết kế

```mermaid
graph TD
    A[Phân tích yêu cầu nghiệp vụ] --> B[Xác định entity và relationship]
    B --> C[Thiết kế normalized schema]
    C --> D[Đánh giá performance requirements]
    D --> E{Performance đủ tốt?}
    E -->|Không| F[Selective denormalization]
    E -->|Có| G[Implement constraints & indexes]
    F --> G
    G --> H[Testing & optimization]
    H --> I[Deploy và monitor]
```

### 🎯 Câu hỏi định hướng khi thiết kế

Trước khi bắt tay vào thiết kế, hãy tự hỏi:

1. **Query patterns**: 80% queries sẽ như thế nào?
2. **Data volume**: Dự đoán lượng dữ liệu sau 1-2 năm?
3. **Read/Write ratio**: Hệ thống read-heavy hay write-heavy?
4. **Concurrency**: Bao nhiêu user đồng thời?
5. **Consistency requirements**: Cần strong consistency hay eventual consistency?
6. **Availability requirements**: Downtime tolerance là bao nhiêu?

---

### 📚 Lý thuyết cốt lõi

#### 1. Cấu trúc cơ sở dữ liệu quan hệ
Cơ sở dữ liệu quan hệ tổ chức dữ liệu thành **bảng (table)**, mỗi bảng đại diện cho một **thực thể (entity)** như *Customer*, *Order*, *Product*. 

**Khái niệm quan trọng:**
- **Khóa chính (Primary Key)**: Định danh duy nhất cho mỗi bản ghi
- **Khóa ngoại (Foreign Key)**: Tham chiếu đến khóa chính của bảng khác
- **Toàn vẹn tham chiếu**: Đảm bảo dữ liệu không "mồ côi"

#### 2. Nguyên tắc chuẩn hóa dữ liệu
**Tại sao cần chuẩn hóa?**
- Tránh trùng lặp dữ liệu
- Đảm bảo tính nhất quán
- Tiết kiệm dung lượng lưu trữ

**Các chuẩn chính:**
- **1NF (First Normal Form)**: Mỗi ô chỉ chứa một giá trị đơn lẻ
- **2NF (Second Normal Form)**: Các cột phụ thuộc hoàn toàn vào khóa chính
- **3NF (Third Normal Form)**: Không có phụ thuộc bắc cầu

#### 3. Lựa chọn kiểu dữ liệu PostgreSQL
| Mục đích | Kiểu dữ liệu | Ví dụ |
|----------|--------------|-------|
| ID tự tăng | `SERIAL`, `BIGSERIAL` | `id SERIAL PRIMARY KEY` |
| Văn bản ngắn | `VARCHAR(n)` | `email VARCHAR(255)` |
| Văn bản dài | `TEXT` | `description TEXT` |
| Số thực | `NUMERIC`, `DECIMAL` | `price NUMERIC(10,2)` |  
| Ngày tháng | `TIMESTAMP`, `DATE` | `created_at TIMESTAMP` |
| JSON | `JSONB` | `metadata JSONB` |

### 💡 Ví dụ minh họa
**Thiết kế bảng Customer:**
```sql
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    phone VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Thiết kế bảng Order với khóa ngoại:**
```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    customer_id INTEGER NOT NULL,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total_amount NUMERIC(10,2) NOT NULL,
    status VARCHAR(20) DEFAULT 'pending',
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

### 🛠️ Thực hành

#### Bài tập 1: Phân tích thiết kế hiện có
Xem xét thiết kế bảng **Clients** và **Contacts** dưới đây:
```sql
-- Bảng có vấn đề về chuẩn hóa
CREATE TABLE bad_design (
    id SERIAL PRIMARY KEY,
    customer_name VARCHAR(100),
    customer_email VARCHAR(255),
    product_list TEXT, -- Vi phạm 1NF: chứa nhiều giá trị
    order_total NUMERIC(10,2),
    product_prices TEXT -- Dữ liệu trùng lặp
);
```

**Nhiệm vụ:** Xác định các vấn đề và đề xuất cách chuẩn hóa.

#### Bài tập 2: Thiết kế từ đầu
Thiết kế schema cho **hệ thống quản lý thư viện** với các yêu cầu:
- Quản lý sách (tên, tác giả, ISBN, thể loại)
- Quản lý thành viên (tên, email, địa chỉ)
- Theo dõi việc mượn sách (ngày mượn, ngày trả dự kiến)

**Hướng dẫn:**
1. Xác định các thực thể chính
2. Liệt kê thuộc tính cho mỗi thực thể
3. Xác định khóa chính cho mỗi bảng
4. Thiết lập mối quan hệ bằng khóa ngoại

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
