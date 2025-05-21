---
layout: archive
title: "Portfolio"
permalink: /portfolio/
author_profile: true
---

------
# [1. Ecommerce shop](/portfolio/project-1/)

## Overview

**Laboratory Shop** is a production‑ready, scalable Telegram‑based vape shop built with FastAPI, PostgreSQL, Redis, Docker and deployed to a Linux server. Originally launched for real‑world users (now closed by the founder), it features:

- **Fully functional online catalog**  
  Browse products, add items to cart, submit orders—all from within Telegram.
- **Scalable, containerized deployment**  
  Each service (Bot, Redis, PostgreSQL) runs in its own Docker container, orchestrated via Docker Compose for easy horizontal scaling.
- **User authentication & order management**  
  Secure login via Telegram OAuth, persistent carts in Redis, and order records in PostgreSQL.
- **Telegram‑based admin dashboard**  
  Managers can view and manage orders, inventory, and customer analytics directly in Telegram (currently migrating to a Django web admin).  
- **Robust data storage**  
  - **PostgreSQL** as the primary relational database for products, users, orders and reviews.  
  - **Redis** for fast, in‑memory cart sessions and rate‑limiting.
- **Clean, modular architecture**  
  Follows SOLID principles and uses SQLAlchemy ORM + Alembic for migrations.
- **CI/CD ready**  
  Automated Docker builds and deployments via GitHub Actions.
  
  [Learn more →](/portfolio/project-1/)

------
