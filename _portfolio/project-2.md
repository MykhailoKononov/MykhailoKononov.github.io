---
title: "Project 2"
excerpt: "A modern FastAPI-based recipe sharing platform with CI/CD, observability, and a clean REST API.<br/><img src='/images/recipe-share-preview.png'>"
collection: portfolio
---

------

<h2>Github Repositiry Link - <a href = "https://github.com/MykhailoKononov/recipe-share-fastapi">https://github.com/MykhailoKononov/recipe-share-fastapi</a></h2>

---

# RecipeShare API Platform

**RecipeShare** is a production‑ready, microservices‑style recipe‑sharing backend built with FastAPI and PostgreSQL. Designed for high throughput and reliability, it features robust API design, comprehensive test coverage, CI/CD automation, and full observability with Prometheus & Grafana.

---
<div style="text-align: center; margin: 1em 0;">
    <h2>Table of Contents</h2>
</div>

1. [Features](#features)  
2. [Architecture & Tech Stack](#architecture--tech-stack)  
3. [API Endpoints & Testing](#api-endpoints--testing)  
4. [Monitoring & Observability](#monitoring--observability)  
5. [Deployment & CI/CD](#deployment--ci-cd)  
6. [Setup & Run](#setup--run)  
7. [Screenshots & Code Snippets](#screenshots--code-snippets)  
8. [Future Improvements](#future-improvements)  

---

<a id="features"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>Features</h2>
</div>
- **RESTful API**  
  - CRUD for recipes, comments, ratings, and user profiles  
  - JWT‑based authentication and role‑based access control  
- **Microservices Architecture**  
  - Separate services for API, Auth, and Image handling  
  - Cloudinary integration for image uploads  
- **Test Coverage**  
  - Pytest suite with fixtures, parametrized tests, and mocks  
  - >90% endpoint coverage  
- **Observability**  
  - Prometheus metrics exported by each service  
  - Grafana dashboards with key performance indicators  
- **Scalable & Containerized**  
  - Docker Compose orchestration (Kubernetes‑ready)  
  - Stateless API pods, shared PostgreSQL database  

---

<a id="architecture--tech-stack"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>Architecture & Tech Stack</h2>
</div>

- **FastAPI**: high‑performance ASGI framework for all services
- **Pytest**: testing framework with coverage reporting
- **PostgreSQL**: relational data store, SQLAlchemy ORM
- **Docker & Docker Compose**: containerization and orchestration
- **GitHub Actions**: pipelines for linting, type checks, tests, builds, and deploys
- **Prometheus & Grafana**: metrics collection and visualization

---

<a id="api-endpoints--testing"></a>
<div style="text-align: center; margin: 1em 0;">
    <h2>API Endpoints & Testing</h2>
</div>

## Link to investigate [auth services](https://github.com/MykhailoKononov/recipe-share-fastapi/tree/master/app/services/auth_services)

- **OAuth2 & JWT**  
  Uses FastAPI’s `OAuth2PasswordBearer` (alias `oauth2_scheme`) to extract bearer tokens. Upon successful login or signup, the API issues a pair of JWT tokens (access + refresh) signed with a secure secret and configurable expiry.
- **Email Confirmation**  
  New users must verify their email via a one‑time link sent to their inbox. The `POST /auth/verify-email` endpoint consumes the token in the link to activate the account.
- **Scoped Access**  
  Endpoints are protected by OAuth2 scopes:  
  - Public (no token) for signup, login, email verification, password reset  
  - `user` scope for recipe creation, commenting, profile updates  
  - `user:verified` to post and edit recipes

### Routes:
- **[Authentication](https://github.com/MykhailoKononov/recipe-share-fastapi/blob/master/app/routes/auth_route.py)**
- **[Profiles & Recipes](https://github.com/MykhailoKononov/recipe-share-fastapi/blob/master/app/routes/profile_route.py)**

### Pytest:

- **[Conftest](https://github.com/MykhailoKononov/recipe-share-fastapi/blob/master/tests/conftest.py)**
  - Spins up a temporary test database in Docker and creates an isolated SQLAlchemy engine & session  
  - Uses fixtures to **truncate** all tables before each test and seed test users/recipes, ensuring full isolation  
- **[Auth test handlers](https://github.com/MykhailoKononov/recipe-share-fastapi/blob/master/tests/test_handlers/test_auth_services.py)**
- **[Peofile & Recipe test handlers](https://github.com/MykhailoKononov/recipe-share-fastapi/blob/master/tests/test_handlers/test_user_profile.py)**
  - Thorough `pytest` modules that exercise each auth endpoint in isolation  
  - Achieves **>90% coverage** for success cases and all expected exceptions (invalid credentials, expired tokens, unverified email, insufficient scopes)  

---

<div style="text-align: center; margin: 1em 0;">
    <h1>Project presentation is still in progress. This page is to be updated soon. Still, you can explore it on my <a href = "https://github.com/MykhailoKononov/recipe-share-fastapi">GitHub Repository</a></h1>
</div>