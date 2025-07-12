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
- **GitLab CI**: pipelines for linting, type checks, tests, builds, and deploys
- **Prometheus & Grafana**: metrics collection and visualization