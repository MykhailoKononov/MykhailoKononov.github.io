---
layout: archive
title: "Portfolio"
permalink: /portfolio/
author_profile: true
---

------
# [1. Ecommerce shop](/portfolio/project-1/)

**Laboratory Shop** is a production‑ready, scalable Telegram‑based vape shop built with FastAPI, PostgreSQL, Redis, Docker and deployed to a Linux server. Originally launched for real‑world users (now closed by the founder), it features:

- **Fully functional online catalog**  
  Browse products, add items to cart, submit orders — all from within Telegram.
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

# [2. FastAPI Recipe Share](/portfolio/project-2/)

**Recipe Share** is a modern web platform that allows users to create, share, and browse recipes with photos and detailed instructions. The project emphasizes **clean REST API design**, **microservice-oriented architecture**, robust **observability** and **СI/CD**.

- **API Design & Development**  
  Well‑structured RESTful endpoints for recipes, user authentication, comments, and ratings—built with FastAPI’s dependency injection and Pydantic models.
- **Test Coverage**  
  Comprehensive pytest suite covering all endpoints with fixtures, parametrized tests, and containerized sessions—maintaining test database.
- **Monitoring & Observability**  
  Prometheus metrics exposed by each service, visualized in Grafana dashboards; structured request logging and alerting via Alertmanager.
- **Scalable Deployment**  
  Containerized microservices orchestrated with Docker Compose (easily portable to Kubernetes), including:
  - **API Service**  
  - **Auth Service**  
  - **Databases** (PostgreSQL)
  - **Grafana** and many other observability services.
- **CI/CD Pipeline**  
  Automated GitLab CI pipelines for linting, testing, building and pushing Docker images to registry, and deploying to staging/production.
  
  [Learn more →](/portfolio/project-2/)