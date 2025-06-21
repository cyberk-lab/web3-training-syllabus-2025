# Triển khai với Prisma ORM & NestJS – Đề cương Buổi Đào tạo (60 phút)

---
### **Giải thích phần tiêu đề**
*Buổi học cuối này kết hợp tất cả kiến thức đã học thành một **production-ready application**. Học viên sẽ học cách triển khai database design với Prisma ORM, tích hợp vào NestJS framework, và deploy lên production environment. Đây là bước cuối cùng để chuyển từ database theory sang working application.*

**Đối tượng học viên:**
Full-stack developers đã nắm vững database design principles và performance optimization, muốn học cách **implement với modern stack** (Prisma + NestJS + PostgreSQL) và **deploy lên production** một cách professional.

**Mục tiêu buổi học:**
- **Thiết lập Prisma ORM** từ ERD design đã có
- **Tích hợp với NestJS** để xây dựng type-safe API
- **Quản lý database migrations** và schema evolution
- **Deploy lên production** với best practices
- **Monitoring và maintenance** database trong production

---

## 1. Dẫn nhập (15 phút)

### **1.1. Khởi động & Câu hỏi mở**
*Ai đã từng gặp những challenge này khi deploy database lên production:*
- **"Schema changes làm crash production database?"** *(Pause để nghe feedback)*
- **"ORM queries không match với optimized SQL đã viết?"**
- **"Database credentials và connection pooling setup như thế nào?"**

*Đây chính là những challenges thực tế khi chuyển từ development sang production. Hôm nay chúng ta sẽ học cách handle những vấn đề này một cách professional.*

### **1.2. Câu chuyện dẫn dắt**
**Prisma's Origin Story - Solving the ORM Problem (2019):**

*Năm 2019, team Prisma gặp phải một vấn đề kinh điển: **"How to bridge the gap between database design và application code?"** Các ORM truyền thống như TypeORM, Sequelize có nhiều limitations:*

- **Type safety issues:** Runtime errors khi schema changes
- **Query performance:** Generated SQL không optimal
- **Migration complexity:** Schema evolution khó maintain
- **Developer experience:** Boilerplate code quá nhiều

*Johannes Schickling (Prisma founder) chia sẻ:*

> *"Chúng tôi muốn tạo ra một tool mà developers có thể **think in database terms** nhưng **work in application terms**. Schema-first approach với auto-generated, type-safe client."*

**Prisma's Innovation:**
1. **Schema-first:** Define database schema, generate application code
2. **Type safety:** 100% TypeScript integration
3. **Query optimization:** Efficient SQL generation
4. **Migration system:** Version-controlled schema evolution

*Kết quả: Prisma được adopt bởi **500,000+ developers** và trở thành standard cho modern Node.js applications.*

### **1.3. Ví dụ hấp dẫn**
**Vercel's Database Architecture với Prisma:**

*Vercel - platform hosting hàng triệu websites - sử dụng Prisma để manage database layer cho internal tools. Impressive numbers:*

**Architecture Highlights:**
```typescript
// Prisma schema cho Vercel's deployment system
model Deployment {
  id        String   @id @default(cuid())
  url       String   @unique
  projectId String
  userId    String
  status    DeploymentStatus
  createdAt DateTime @default(now())
  
  project   Project  @relation(fields: [projectId], references: [id])
  user      User     @relation(fields: [userId], references: [id])
  
  @@index([projectId, status])
  @@index([userId, createdAt])
}
```

**Performance Results:**
- **Deployment queries:** < 5ms average response time
- **Type safety:** Zero runtime type errors in production
- **Developer velocity:** 50% faster feature development
- **Database operations:** 10,000+ deployments/day seamlessly

*Vercel chứng minh: **Modern ORM + Good database design = Production excellence.***

### **1.4. Giới thiệu chủ đề**
*"Hôm nay chúng ta sẽ complete journey từ database design đến production application. Chúng ta sẽ học setup Prisma từ ERD, integrate với NestJS để build type-safe APIs, handle migrations, và deploy lên production với monitoring. Cuối buổi, mọi người sẽ có một complete application stack ready for real users."*

---

## 2. Nguyên tắc & Quy trình cốt lõi (20 phút)

### **2.1. Prisma Setup & Schema Design**

#### **From ERD to Prisma Schema:**

**Step 1: Project Initialization**
```bash
# Create new NestJS project
npm i -g @nestjs/cli
nest new food-delivery-api

# Install Prisma
npm install prisma @prisma/client
npm install -D prisma

# Initialize Prisma
npx prisma init
```

**Step 2: Database Configuration**
```env
# .env
DATABASE_URL="postgresql://username:password@localhost:5432/food_delivery"
NODE_ENV="development"
```

**Step 3: Schema Definition từ ERD Design**
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
  addresses Json?    // JSONB for flexible address storage
  createdAt DateTime @default(now()) @map("created_at")
  updatedAt DateTime @updatedAt @map("updated_at")
  
  // Relationships
  orders    Order[]
  reviews   Review[]
  
  @@map("customers")
}

model Restaurant {
  id          Int     @id @default(autoincrement())
  name        String  @db.VarChar(100)
  address     String  @db.VarChar(255)
  phone       String  @db.VarChar(20)
  cuisineType String  @db.VarChar(50) @map("cuisine_type")
  avgRating   Decimal @default(0) @db.Decimal(2, 1) @map("avg_rating")
  totalOrders Int     @default(0) @map("total_orders") // Denormalized
  isActive    Boolean @default(true) @map("is_active")
  createdAt   DateTime @default(now()) @map("created_at")
  
  // Relationships
  menu        Menu?
  orders      Order[]
  reviews     Review[]
  
  // Indexes for performance
  @@index([cuisineType])
  @@index([avgRating])
  @@map("restaurants")
}

model Menu {
  id           Int    @id @default(autoincrement())
  restaurantId Int    @unique @map("restaurant_id")
  name         String @db.VarChar(100)
  description  String?
  
  // Relationships
  restaurant   Restaurant @relation(fields: [restaurantId], references: [id], onDelete: Cascade)
  dishes       Dish[]
  
  @@map("menus")
}

model Dish {
  id          Int     @id @default(autoincrement())
  menuId      Int     @map("menu_id")
  name        String  @db.VarChar(100)
  description String?
  price       Decimal @db.Decimal(8, 2)
  imageUrl    String? @db.VarChar(255) @map("image_url")
  isAvailable Boolean @default(true) @map("is_available")
  category    String  @db.VarChar(50) // Denormalized for simplicity
  
  // Relationships
  menu        Menu        @relation(fields: [menuId], references: [id], onDelete: Cascade)
  orderItems  OrderItem[]
  
  // Indexes
  @@index([menuId, isAvailable])
  @@index([category])
  @@map("dishes")
}

model Order {
  id              Int      @id @default(autoincrement())
  customerId      Int      @map("customer_id")
  restaurantId    Int      @map("restaurant_id")
  driverId        Int?     @map("driver_id")
  orderTime       DateTime @default(now()) @map("order_time")
  totalAmount     Decimal  @db.Decimal(10, 2) @map("total_amount")
  deliveryFee     Decimal  @db.Decimal(6, 2) @map("delivery_fee")
  status          OrderStatus @default(PENDING)
  deliveryAddress Json     @map("delivery_address") // JSONB
  
  // Denormalized fields for performance
  customerName    String?  @db.VarChar(100) @map("customer_name")
  restaurantName  String?  @db.VarChar(100) @map("restaurant_name")
  
  // Relationships
  customer        Customer    @relation(fields: [customerId], references: [id])
  restaurant      Restaurant  @relation(fields: [restaurantId], references: [id])
  driver          Driver?     @relation(fields: [driverId], references: [id])
  orderItems      OrderItem[]
  
  // Indexes for common queries
  @@index([customerId, status])
  @@index([restaurantId, orderTime])
  @@index([driverId, status])
  @@index([orderTime])
  @@map("orders")
}

model OrderItem {
  orderId      Int     @map("order_id")
  dishId       Int     @map("dish_id")
  quantity     Int
  unitPrice    Decimal @db.Decimal(8, 2) @map("unit_price") // Historical pricing
  
  // Relationships
  order        Order   @relation(fields: [orderId], references: [id], onDelete: Cascade)
  dish         Dish    @relation(fields: [dishId], references: [id])
  
  @@id([orderId, dishId])
  @@map("order_items")
}

model Driver {
  id            Int      @id @default(autoincrement())
  name          String   @db.VarChar(100)
  phone         String   @unique @db.VarChar(20)
  licenseNumber String   @unique @db.VarChar(50) @map("license_number")
  vehicleType   String   @db.VarChar(50) @map("vehicle_type")
  status        DriverStatus @default(OFFLINE)
  currentLat    Decimal? @db.Decimal(10, 8) @map("current_lat")
  currentLng    Decimal? @db.Decimal(11, 8) @map("current_lng")
  
  // Relationships
  orders        Order[]
  
  @@index([status])
  @@map("drivers")
}

model Review {
  id           Int      @id @default(autoincrement())
  customerId   Int      @map("customer_id")
  restaurantId Int      @map("restaurant_id")
  rating       Int      // 1-5 stars
  comment      String?
  createdAt    DateTime @default(now()) @map("created_at")
  
  // Relationships
  customer     Customer   @relation(fields: [customerId], references: [id])
  restaurant   Restaurant @relation(fields: [restaurantId], references: [id])
  
  // Business rule: One review per customer per restaurant
  @@unique([customerId, restaurantId])
  @@index([restaurantId, rating])
  @@map("reviews")
}

// Enums
enum OrderStatus {
  PENDING
  CONFIRMED
  PREPARING
  READY
  PICKED_UP
  DELIVERED
  CANCELLED
}

enum DriverStatus {
  OFFLINE
  AVAILABLE
  BUSY
}
```

### **2.2. NestJS Integration**

#### **Prisma Service Setup:**

```typescript
// src/prisma/prisma.service.ts
import { Injectable, OnModuleInit, OnModuleDestroy } from '@nestjs/common';
import { PrismaClient } from '@prisma/client';

@Injectable()
export class PrismaService extends PrismaClient implements OnModuleInit, OnModuleDestroy {
  constructor() {
    super({
      log: ['query', 'info', 'warn', 'error'],
      datasources: {
        db: {
          url: process.env.DATABASE_URL,
        },
      },
    });
  }

  async onModuleInit() {
    // Query logging for development
    if (process.env.NODE_ENV === 'development') {
      this.$on('query', (e) => {
        console.log('Query: ' + e.query);
        console.log('Duration: ' + e.duration + 'ms');
      });
    }
    
    await this.$connect();
  }

  async onModuleDestroy() {
    await this.$disconnect();
  }

  // Utility methods
  async cleanDatabase() {
    if (process.env.NODE_ENV === 'production') return;
    
    const tablenames = await this.$queryRaw<Array<{ tablename: string }>>`
      SELECT tablename FROM pg_tables WHERE schemaname='public'
    `;
    
    for (const { tablename } of tablenames) {
      if (tablename !== '_prisma_migrations') {
        try {
          await this.$executeRawUnsafe(`TRUNCATE TABLE "public"."${tablename}" CASCADE;`);
        } catch (error) {
          console.log({ error });
        }
      }
    }
  }
}
```

#### **Module Setup:**

```typescript
// src/prisma/prisma.module.ts
import { Global, Module } from '@nestjs/common';
import { PrismaService } from './prisma.service';

@Global()
@Module({
  providers: [PrismaService],
  exports: [PrismaService],
})
export class PrismaModule {}
```

### **2.3. CRUD Operations với Type Safety**

#### **Restaurant Service Example:**

```typescript
// src/restaurants/restaurants.service.ts
import { Injectable, NotFoundException } from '@nestjs/common';
import { PrismaService } from '../prisma/prisma.service';
import { CreateRestaurantDto, UpdateRestaurantDto, RestaurantQueryDto } from './dto';
import { Prisma } from '@prisma/client';

@Injectable()
export class RestaurantsService {
  constructor(private prisma: PrismaService) {}

  async create(createRestaurantDto: CreateRestaurantDto) {
    return this.prisma.restaurant.create({
      data: {
        ...createRestaurantDto,
        menu: {
          create: {
            name: `${createRestaurantDto.name} Menu`,
            description: 'Main menu'
          }
        }
      },
      include: {
        menu: true
      }
    });
  }

  async findAll(query: RestaurantQueryDto) {
    const { page = 1, limit = 10, cuisineType, search, sortBy = 'avgRating' } = query;
    const skip = (page - 1) * limit;

    const where: Prisma.RestaurantWhereInput = {
      isActive: true,
      ...(cuisineType && { cuisineType }),
      ...(search && {
        OR: [
          { name: { contains: search, mode: 'insensitive' } },
          { address: { contains: search, mode: 'insensitive' } }
        ]
      })
    };

    const orderBy: Prisma.RestaurantOrderByWithRelationInput = {};
    if (sortBy === 'avgRating') {
      orderBy.avgRating = 'desc';
    } else if (sortBy === 'totalOrders') {
      orderBy.totalOrders = 'desc';
    } else {
      orderBy.name = 'asc';
    }

    const [restaurants, total] = await Promise.all([
      this.prisma.restaurant.findMany({
        where,
        orderBy,
        skip,
        take: limit,
        include: {
          menu: {
            include: {
              dishes: {
                where: { isAvailable: true },
                take: 5, // Preview dishes
                orderBy: { price: 'asc' }
              }
            }
          },
          _count: {
            select: { orders: true, reviews: true }
          }
        }
      }),
      this.prisma.restaurant.count({ where })
    ]);

    return {
      data: restaurants,
      pagination: {
        page,
        limit,
        total,
        totalPages: Math.ceil(total / limit)
      }
    };
  }

  async findOne(id: number) {
    const restaurant = await this.prisma.restaurant.findUnique({
      where: { id },
      include: {
        menu: {
          include: {
            dishes: {
              where: { isAvailable: true },
              orderBy: { category: 'asc' }
            }
          }
        },
        reviews: {
          include: {
            customer: {
              select: { name: true }
            }
          },
          orderBy: { createdAt: 'desc' },
          take: 10
        }
      }
    });

    if (!restaurant) {
      throw new NotFoundException(`Restaurant with ID ${id} not found`);
    }

    return restaurant;
  }

  async update(id: number, updateRestaurantDto: UpdateRestaurantDto) {
    try {
      return await this.prisma.restaurant.update({
        where: { id },
        data: updateRestaurantDto,
        include: {
          menu: true
        }
      });
    } catch (error) {
      if (error instanceof Prisma.PrismaClientKnownRequestError) {
        if (error.code === 'P2025') {
          throw new NotFoundException(`Restaurant with ID ${id} not found`);
        }
      }
      throw error;
    }
  }

  async remove(id: number) {
    try {
      return await this.prisma.restaurant.update({
        where: { id },
        data: { isActive: false } // Soft delete
      });
    } catch (error) {
      if (error instanceof Prisma.PrismaClientKnownRequestError) {
        if (error.code === 'P2025') {
          throw new NotFoundException(`Restaurant with ID ${id} not found`);
        }
      }
      throw error;
    }
  }

  // Complex business logic
  async updateRating(restaurantId: number) {
    const stats = await this.prisma.review.aggregate({
      where: { restaurantId },
      _avg: { rating: true },
      _count: { rating: true }
    });

    return this.prisma.restaurant.update({
      where: { id: restaurantId },
      data: {
        avgRating: stats._avg.rating || 0,
        totalOrders: stats._count.rating
      }
    });
  }
}
```

### **2.4. Advanced Prisma Features**

#### **Transactions & Complex Operations:**

```typescript
// src/orders/orders.service.ts
async createOrder(customerId: number, createOrderDto: CreateOrderDto) {
  return this.prisma.$transaction(async (tx) => {
    // 1. Validate customer exists
    const customer = await tx.customer.findUnique({
      where: { id: customerId }
    });
    if (!customer) throw new NotFoundException('Customer not found');

    // 2. Validate dishes and calculate total
    const dishes = await tx.dish.findMany({
      where: {
        id: { in: createOrderDto.items.map(item => item.dishId) },
        isAvailable: true
      }
    });

    if (dishes.length !== createOrderDto.items.length) {
      throw new BadRequestException('Some dishes are not available');
    }

    let totalAmount = 0;
    const orderItems = createOrderDto.items.map(item => {
      const dish = dishes.find(d => d.id === item.dishId);
      const itemTotal = dish.price.toNumber() * item.quantity;
      totalAmount += itemTotal;
      
      return {
        dishId: item.dishId,
        quantity: item.quantity,
        unitPrice: dish.price
      };
    });

    // 3. Create order with items
    const order = await tx.order.create({
      data: {
        customerId,
        restaurantId: createOrderDto.restaurantId,
        totalAmount,
        deliveryFee: 2.99, // Fixed delivery fee
        deliveryAddress: createOrderDto.deliveryAddress,
        customerName: customer.name, // Denormalized
        orderItems: {
          create: orderItems
        }
      },
      include: {
        orderItems: {
          include: {
            dish: true
          }
        },
        customer: true,
        restaurant: true
      }
    });

    // 4. Update restaurant total orders (denormalized)
    await tx.restaurant.update({
      where: { id: createOrderDto.restaurantId },
      data: {
        totalOrders: { increment: 1 }
      }
    });

    return order;
  });
}
```

#### **Raw Queries cho Complex Analytics:**

```typescript
// src/analytics/analytics.service.ts
async getRevenueAnalytics(restaurantId: number, period: 'day' | 'week' | 'month') {
  const interval = period === 'day' ? '1 day' : period === 'week' ? '7 days' : '30 days';
  
  const result = await this.prisma.$queryRaw<Array<{
    date: Date;
    total_orders: number;
    total_revenue: number;
    avg_order_value: number;
  }>>`
    SELECT 
      DATE_TRUNC(${period}, order_time) as date,
      COUNT(*)::int as total_orders,
      SUM(total_amount)::float as total_revenue,
      AVG(total_amount)::float as avg_order_value
    FROM orders 
    WHERE restaurant_id = ${restaurantId}
      AND order_time >= NOW() - INTERVAL ${interval}
      AND status = 'DELIVERED'
    GROUP BY DATE_TRUNC(${period}, order_time)
    ORDER BY date DESC;
  `;

  return result;
}
```

---

## 3. Áp dụng thực tế & Case studies (15 phút)

### **3.1. Migration Management Strategy**

#### **Development to Production Migration Flow:**

```mermaid
graph TD
    A["💻 Development<br/>Schema changes"] --> B["🔄 Generate Migration<br/>prisma migrate dev"] 
    B --> C["🧪 Test Migration<br/>Staging environment"]
    C --> D["📋 Review Migration<br/>SQL review process"]
    D --> E["🚀 Deploy Migration<br/>prisma migrate deploy"]
    E --> F["📊 Monitor<br/>Performance impact"]
    
    style A fill:#e3f2fd
    style B fill:#fff3e0  
    style C fill:#e8f5e8
    style D fill:#ffeb3b
    style E fill:#4caf50
    style F fill:#ff9800
```

#### **Migration Best Practices:**

**1. Safe Schema Changes:**
```prisma
// ✅ SAFE: Adding optional fields
model Customer {
  id        Int      @id @default(autoincrement())
  name      String
  email     String   @unique
  phone     String?  // Optional field - safe to add
  createdAt DateTime @default(now())
}

// ❌ RISKY: Dropping columns without backup
model Customer {
  id        Int      @id @default(autoincrement())
  name      String
  email     String   @unique
  // phone     String?  // Dropping - data loss!
  createdAt DateTime @default(now())
}
```

**2. Multi-step Migration for Breaking Changes:**
```sql
-- Step 1: Add new column
ALTER TABLE customers ADD COLUMN full_name VARCHAR(200);

-- Step 2: Populate data (background job)
UPDATE customers SET full_name = CONCAT(first_name, ' ', last_name);

-- Step 3: Make column required (separate migration)
ALTER TABLE customers ALTER COLUMN full_name SET NOT NULL;

-- Step 4: Drop old columns (separate migration)
ALTER TABLE customers DROP COLUMN first_name, DROP COLUMN last_name;
```

**3. Migration Scripts:**
```typescript
// scripts/migrate-production.ts
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function main() {
  console.log('Starting production migration...');
  
  // Pre-migration checks
  const tableCount = await prisma.$queryRaw`SELECT COUNT(*) FROM information_schema.tables WHERE table_schema = 'public'`;
  console.log(`Current tables: ${tableCount}`);
  
  // Run migration
  await prisma.$executeRaw`-- Your migration SQL here`;
  
  // Post-migration validation
  const newTableCount = await prisma.$queryRaw`SELECT COUNT(*) FROM information_schema.tables WHERE table_schema = 'public'`;
  console.log(`Tables after migration: ${newTableCount}`);
  
  console.log('Migration completed successfully!');
}

main()
  .catch((e) => {
    console.error('Migration failed:', e);
    process.exit(1);
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
```

### **3.2. Production Deployment Setup**

#### **Environment Configuration:**

```typescript
// src/config/database.config.ts
import { registerAs } from '@nestjs/config';

export default registerAs('database', () => ({
  url: process.env.DATABASE_URL,
  maxConnections: parseInt(process.env.DB_MAX_CONNECTIONS) || 10,
  connectionTimeout: parseInt(process.env.DB_CONNECTION_TIMEOUT) || 20000,
  ssl: process.env.NODE_ENV === 'production' ? { rejectUnauthorized: false } : false,
  logging: process.env.NODE_ENV === 'development',
}));
```

#### **Docker Setup:**

```dockerfile
# Dockerfile
FROM node:18-alpine AS builder

WORKDIR /app
COPY package*.json ./
COPY prisma ./prisma/
RUN npm ci

COPY . .
RUN npm run build
RUN npx prisma generate

FROM node:18-alpine AS production

WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules/.prisma ./node_modules/.prisma
COPY --from=builder /app/prisma ./prisma

EXPOSE 3000
CMD ["node", "dist/main.js"]
```

```yaml
# docker-compose.yml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgresql://user:password@db:5432/food_delivery
      - NODE_ENV=production
    depends_on:
      - db
      - redis
    restart: unless-stopped

  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=food_delivery
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "5432:5432"

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data

volumes:
  postgres_data:
  redis_data:
```

#### **CI/CD Pipeline:**

```yaml
# .github/workflows/deploy.yml
name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_PASSWORD: postgres
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'

      - run: npm ci
      - run: npx prisma generate
      - run: npx prisma db push
        env:
          DATABASE_URL: postgresql://postgres:postgres@localhost:5432/test
      - run: npm run test:e2e

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to production
        run: |
          # Deploy script here
          echo "Deploying to production..."
```

### **3.3. Monitoring & Maintenance**

#### **Health Checks:**

```typescript
// src/health/health.controller.ts
import { Controller, Get } from '@nestjs/common';
import { HealthCheck, HealthCheckService, PrismaHealthIndicator } from '@nestjs/terminus';
import { PrismaService } from '../prisma/prisma.service';

@Controller('health')
export class HealthController {
  constructor(
    private health: HealthCheckService,
    private prismaHealth: PrismaHealthIndicator,
    private prisma: PrismaService,
  ) {}

  @Get()
  @HealthCheck()
  check() {
    return this.health.check([
      () => this.prismaHealth.pingCheck('database', this.prisma),
      () => this.checkDatabaseConnections(),
    ]);
  }

  private async checkDatabaseConnections() {
    const connections = await this.prisma.$queryRaw<Array<{ count: number }>>`
      SELECT COUNT(*) as count FROM pg_stat_activity WHERE state = 'active';
    `;
    
    const activeConnections = connections[0].count;
    const maxConnections = 100; // Your max connection limit
    
    const isHealthy = activeConnections < maxConnections * 0.8;
    
    return {
      'database-connections': {
        status: isHealthy ? 'up' : 'down',
        message: `${activeConnections}/${maxConnections} connections active`,
      },
    };
  }
}
```

#### **Performance Monitoring:**

```typescript
// src/common/interceptors/performance.interceptor.ts
import { Injectable, NestInterceptor, ExecutionContext, CallHandler, Logger } from '@nestjs/common';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class PerformanceInterceptor implements NestInterceptor {
  private readonly logger = new Logger(PerformanceInterceptor.name);

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    const request = context.switchToHttp().getRequest();
    const { method, url } = request;
    const startTime = Date.now();

    return next.handle().pipe(
      tap(() => {
        const endTime = Date.now();
        const duration = endTime - startTime;
        
        if (duration > 1000) { // Log slow requests
          this.logger.warn(`Slow request: ${method} ${url} took ${duration}ms`);
        }
        
        // Send to monitoring service
        this.sendMetrics(method, url, duration);
      }),
    );
  }

  private sendMetrics(method: string, url: string, duration: number) {
    // Send to your monitoring service (DataDog, New Relic, etc.)
    // Example: this.metricsService.timing('api.request.duration', duration, { method, url });
  }
}
```

---

## 4. Thảo luận mở & Workshop mini (7 phút)

### **Workshop: Production Deployment Challenge**

**Scenario:** *Bạn cần deploy food delivery API lên production với 1000+ concurrent users. Database có 100K+ records và cần zero-downtime deployment.*

#### **Câu hỏi thảo luận:**

1. **Migration Strategy:**
   *"Bạn cần thêm một column 'delivery_zone' vào bảng restaurants có 10K records. Làm sao deploy migration này mà không downtime?"*

   **Gợi ý trả lời:**
   - **Step 1:** Add optional column với default value
   - **Step 2:** Background job populate data
   - **Step 3:** Separate deployment make column required
   - **Step 4:** Update application logic to use new column

2. **Connection Pooling:**
   *"Với 1000 concurrent users, làm sao config connection pool để optimal performance mà không overwhelm database?"*

   **Gợi ý trả lời:**
   - **Connection pool size:** 10-20 connections per app instance
   - **Connection timeout:** 20-30 seconds
   - **Idle timeout:** 10 minutes
   - **Load balancer:** Multiple app instances behind load balancer

3. **Monitoring Setup:**
   *"Metrics nào quan trọng nhất để monitor trong production? Làm sao set up alerting?"*

   **Gợi ý trả lời:**
   - **Response time:** API endpoints < 500ms
   - **Database connections:** < 80% pool utilization
   - **Error rate:** < 1% for critical endpoints
   - **Query performance:** Slow queries > 1 second

**Interactive Exercise (3 phút):**
*Hãy design một deployment strategy cho schema change sau:*

```prisma
// Current schema
model Order {
  id          Int     @id @default(autoincrement())
  totalAmount Decimal @db.Decimal(10, 2)
  // ... other fields
}

// New schema - breaking change
model Order {
  id           Int     @id @default(autoincrement())
  subtotal     Decimal @db.Decimal(10, 2)  // New field
  tax          Decimal @db.Decimal(10, 2)  // New field
  deliveryFee  Decimal @db.Decimal(10, 2)  // New field
  totalAmount  Decimal @db.Decimal(10, 2)  // Calculated field
  // ... other fields
}
```

**Sample Solution:**
```sql
-- Migration 1: Add new columns
ALTER TABLE orders ADD COLUMN subtotal DECIMAL(10,2);
ALTER TABLE orders ADD COLUMN tax DECIMAL(10,2);
ALTER TABLE orders ADD COLUMN delivery_fee DECIMAL(10,2);

-- Migration 2: Populate data (background job)
UPDATE orders SET 
  subtotal = total_amount * 0.85,
  tax = total_amount * 0.10,
  delivery_fee = total_amount * 0.05;

-- Migration 3: Make columns required
ALTER TABLE orders ALTER COLUMN subtotal SET NOT NULL;
ALTER TABLE orders ALTER COLUMN tax SET NOT NULL;
ALTER TABLE orders ALTER COLUMN delivery_fee SET NOT NULL;
```

---

## 5. Tóm tắt (3 phút)

### **5.1. Tổng kết các nguyên tắc chính**
- **Schema-first Development:** Prisma schema as single source of truth
- **Type Safety:** End-to-end type safety từ database đến API
- **Migration Strategy:** Safe, incremental changes với zero downtime
- **Production Ready:** Monitoring, health checks, performance optimization

### **5.2. Nhấn mạnh mindset cốt lõi**
**"Modern database development is about developer experience và production reliability. Prisma + NestJS gives you both."**

### **5.3. Kết thúc journey**
*"Chúng ta đã complete journey từ database design principles → ERD design → Performance optimization → Production deployment. Bây giờ bạn có đầy đủ skills để build và maintain production-ready database applications!"*

---

## 6. Tài liệu tham khảo & Next steps

### **Tools và Resources:**
- **Prisma Documentation:** Complete guide và best practices
- **NestJS + Prisma Integration:** Official integration guide
- **PostgreSQL Production Tuning:** Performance optimization
- **Docker & Kubernetes:** Container deployment strategies

### **Practice Exercises:**
- **Exercise 1:** Deploy complete food delivery API lên cloud platform
- **Exercise 2:** Set up comprehensive monitoring và alerting
- **Exercise 3:** Implement advanced features (caching, real-time updates)

### **Advanced Topics:**
- **Database Scaling:** Read replicas, connection pooling
- **Microservices:** Database per service pattern
- **Event Sourcing:** Advanced data modeling patterns
- **GraphQL Integration:** Prisma + GraphQL + NestJS 