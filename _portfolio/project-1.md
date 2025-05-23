---
title: "Project 1"
excerpt: "Short description of portfolio item number 1<br/><img src='/images/500x300.png'>"
collection: portfolio
---

------

# Laboratory Shop

**Laboratory Shop** is a production‑ready, scalable Telegram‑based ecommerce bot for vape products. Built with FastAPI, PostgreSQL, Redis, and Docker, it was actively used by real customers before being closed by the founder. This page dives into the architecture, key modules, and code snippets that demonstrate how the system works under the hood.

---

<div style="text-align: center; margin: 1em 0;">
    <h2>Table of Contents</h2>
</div>

1. [Features](#features)
2. [Architecture & Tech Stack](#architecture--tech-stack)
3. [Database Schema](#database-schema)
4. [Core Modules](#core-modules)
   - [Main Shop Handlers](#main-shop-handlers)
   - [Order Flow & Cart Management](#order-flow--cart-management)
   - [Admin Dashboard](#admin-dashboard)
5. [Deployment](#deployment)
8. [Future Improvements](#future-improvements)

---

<a id="features"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>Features</h2>
</div>

- **User Shopping Flow**  
  - Browse products by category  
  - Add/remove items in cart  
  - Checkout with address or postal office selection  
- **Session Management**  
  - Persistent carts in Redis for each user  
  - Rate‑limiting and session expiry  
- **Admin Dashboard**  
  - Approve/reject orders  
  - Inventory management  
  - View sales & customer analytics  
- **Notifications**  
  - Order status updates via Telegram  
  - Low‑stock alerts  
- **Security**  
  - Telegram OAuth for user identity  
  - Role‑based access for admins  

---

<a id="architecture--tech-stack"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>Architecture & Tech Stack</h2>
</div>


```plaintext
┌───────────────┐     ┌──────────┐     ┌───────────────┐
│ Telegram User │⇄    │ Bot API  │⇄   │ PostgreSQL DB │
│  (aiogram)    │     │(FastAPI) │     │ with SQLAlchemy│
└───────────────┘     └──────────┘     └───────────────┘
                        │
                        │ Redis (Cart sessions, rate‑limit)
                        ↓
                    ┌────────┐
                    │ Admin  │
                    │Frontend│
                    └────────┘
```

- **Aiogram:** handles Telegram message & callback queries

- **PostgreSQL + SQLAlchemy + Alembic:** relational database & migrations

- **Redis:** in‑memory cart/session storage, rate‑limiting

- **Docker & Docker Compose:** containerization and service orchestration

- **AWS EC2:** Linux-based VPS

- **Cloudinary:** Photo-storing

- **GitHub Actions:** CI/CD for building & pushing Docker images (in progress)

---

<a id="database-schema"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>Database Schema</h2>
</div>

[Link to code snippet](https://gist.github.com/MykhailoKononov/587b3a21c89eb855c48b11c4c3d76c91)

| Table           | Description                                                                               |
| --------------- | ------------------------------------------------------------------------------------------|
| `clients`       | Stores Telegram users (clients and managers), their roles and profile metadata            |
| `items`         | Base table for all shop products (common fields, polymorphic parent)                      |
| `liquids`       | Polymorphic of `items` for e‑liquid products (brand, flavor, volume, nicotine)            |
| `disposable`    | Polymorphic of `items` for disposable vape devices (brand, model, flavor, puffs, nicotine)|
| `cartridges`    | Polymorphic of `items` for replaceable cartridges (brand, model, compatibility)           |
| `pod_systems`   | Polymorphic of `items` for pod systems (brand, model)                                     |
| `suppliers`     | Vendors supplying inventory (name, contact info)                                          |
| `supplies`      | Records of stock deliveries from suppliers (item, supplier, quantity, cost, date)         |
| `orders`        | Customer orders (client info, delivery details, status, assigned manager, promo code)     |
| `order_items`   | Line‑items for each order (which item, quantity, sale price)                              |
| `promo_code`    | Promotional codes (type, value, validity, usage status, associated client)                |

---
<a id="core-modules"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>Core Modules</h2>
</div>

- ### [Main Shop Handlers](https://gist.github.com/MykhailoKononov/4a375e63d5569be6dc86af41db957692)
    - This module contains all the Telegram bot command and callback handlers powered by **Aiogram**. It routes user messages, presents product catalogs, processes “Add to Cart” actions and navigates users through the shop flow. Handlers are organized by feature (e.g. `shop_handlers`, `cart_handlers`, `checkout_handlers`) and each exposes clear entry points:

    - [Link](https://gist.github.com/MykhailoKononov/4a375e63d5569be6dc86af41db957692) to code snippet for `shop_handlers`

    <h3>Video Demonstration</h3>

    <div class="embed-container">
        <iframe src="https://drive.google.com/file/d/1Ec_4aB52Om-zHYhnzSE8C4vnKvmyd_2m/preview" allowfullscreen="true" style="width:100%; height:500px;"></iframe>
    </div>

---

- ### [Order Flow](https://gist.github.com/MykhailoKononov/8ba13f20aa66dad3a61dbf8b5f04a9b0) & [Cart Management](https://gist.github.com/MykhailoKononov/ad0bbdc70d894a0aa467346ad3506cde)
    - This service layer handles all cart operations and checkout logic, using Redis for fast, in‑memory session storage. Key responsibilities include storing per‑user carts, enforcing TTL expiration, calculating totals, and orchestrating the creation of Order and OrderItem records in PostgreSQL via SQLAlchemy:

    - [Link](https://gist.github.com/MykhailoKononov/8ba13f20aa66dad3a61dbf8b5f04a9b0) to code snippet for `cart_handlers`
    - [Link](https://gist.github.com/MykhailoKononov/ad0bbdc70d894a0aa467346ad3506cde) to code snippet for `cart_redis`

    <h3>Video Demonstration</h3>

    <div class="embed-container">
        <iframe src="https://drive.google.com/file/d/1F_Vxg4P7diTBV5j0VIcQNewhzwYKyFHW/preview" allowfullscreen="true"   style="width:100%; height:500px;"></iframe>
    </div>

---

- ### Admin Dashboard
    - All administrative functions are handled directly through the Telegram bot, allowing managers to:
        1. **Manage Inventory**
            - Add new products or update existing item details (price, stock, description)
            - Record incoming supplies and adjust stock levels on the fly
        2. **Process Orders**
            - View incoming order requests with full details (user info, delivery method, cart contents)
            - Approve or reject orders, with automatic status updates sent to customers
            - Track order history and filter by status, date, or manager
        3. **Issue Promo Codes**
            - Generate and revoke promotional codes from within the bot interface
            - Set code parameters (discount value, expiry date, usage limits) 


    - [Link](https://gist.github.com/MykhailoKononov/867dd3cb5266852da368cd041723a815) to code snippet for `admin/order`
    - [Link](https://gist.github.com/MykhailoKononov/c74e682d07b171daaeecda761fe32f29) to code snippet for `admin/supply`

    <h3>Video Demonstration (from manager's account)</h3>

    <div class="embed-container">
        <iframe src="https://drive.google.com/file/d/1DCb2FyvPkEeqb1BbjWzGTSaVKfa14s6Z/preview" allowfullscreen="true"   style="width:100%; height:500px;"></iframe>
    </div>

---
<a id="deployment"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>Deployment</h2>
</div>

Services are defined in docker-compose.yml:

```python
services:
  redis:
    image: redis:latest
    container_name: redis
    command: redis-server --save 60 1 --loglevel warning
    restart: on-failure
    ports:
      - "6379:6379"
    networks:
      - bot_network

  db:
    image: postgres:16-alpine
    container_name: db
    restart: on-failure
    env_file:
      - .env
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - bot_network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}"]
      interval: 5s
      timeout: 5s
      retries: 5

  bot:
    build: .
    container_name: bot
    command: sh -c "make migrate && python -m main"
    env_file:
      - .env
    volumes:
      - ./migrations:/migrations
    restart: always
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started
    networks:
      - bot_network

volumes:
  pgdata:

networks:
  bot_network:
    driver: bridge
```

To deploy on your Linux server:

1. Clone repo
2. Set environment variables
3. docker-compose up -d --build


---
<a id="future-improvements"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>Future Improvements</h2>
</div>

- Migrate Admin from Telegram → Django web admin
- Integrate payment processing (Stripe, crypto)
- Add user reviews & ratings in bot
- Horizontal scaling with Kubernetes