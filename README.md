<div align="center">

# 🌉 CodeBridges (Codebridge404)
### Enterprise Multi-Tenant SaaS Platform for Modern Retail, POS & Operations

[![Next.js](https://img.shields.io/badge/Next.js-16.2-black?style=for-the-badge&logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![Laravel](https://img.shields.io/badge/Laravel-11-FF2D20?style=for-the-badge&logo=laravel)](https://laravel.com/)
[![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?style=for-the-badge&logo=php&logoColor=white)](https://php.net/)
[![Docker](https://img.shields.io/badge/Docker-Microservices-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Bakong KHQR](https://img.shields.io/badge/Payment-Bakong_KHQR-E02424?style=for-the-badge)](https://bakong.nbc.gov.kh/)

<p align="center">
  A cloud-native, distributed microservice enterprise management system featuring high-throughput Point of Sale (POS), Kitchen Display Systems (KDS), Customer-Facing Displays (CFD), multi-outlet inventory, and real-time Bakong KHQR dynamic cashless payments.
</p>

---

</div>

## 📑 Core Repositories

| Repository | Description | Primary Stack | Default / Staging Branch |
| :--- | :--- | :--- | :--- |
| [**`codebridgesfront`**](https://github.com/Codebridge404/codebridgesfront) | Modern high-performance web client, POS terminal UI, and Organization management dashboard. | Next.js 16, React 19, Tailwind CSS 4, Framer Motion | `master` / `demo` |
| [**`codebridge-services`**](https://github.com/Codebridge404/codebridge-services) | Distributed microservices backend architecture powered by Docker, Laravel 11, Redis, and Horizon. | Laravel 11, PHP 8.2, Docker Compose, MySQL, Redis | `master` / `demo` |

---

## 🏛️ System Architecture

```mermaid
graph TD
    Client["Client / Browser / POS Terminal<br/>(Port 3000)"]
    Gateway["API Gateway / Reverse Proxy<br/>(Port 8000)"]
    
    subgraph Services["Core Microservices"]
        AuthService["Auth & Identity Service<br/>(Port 8001)<br/>Multi-Tenancy, Users, Roles, Outlets"]
        OpsService["Operations Service<br/>(Port 8002)<br/>POS, Sales, Products, Inventory, Shifts"]
    end

    subgraph DataTier["Data & Queue Tier"]
        AuthDB[("Auth MySQL DB")]
        OpsDB[("Operations MySQL DB")]
        AuthRedis[("Auth Redis & Horizon")]
        OpsRedis[("Operations Redis & Horizon")]
    end

    subgraph Payments["External Gateways"]
        Bakong["National Bank of Cambodia<br/>Bakong KHQR API"]
    end

    Client -->|HTTP / REST| Gateway
    Client -->|Direct WebSocket / Events| Services
    Gateway -->|Route /api/v1/auth| AuthService
    Gateway -->|Route /api/v1/operations| OpsService
    AuthService --> AuthDB
    AuthService --> AuthRedis
    OpsService --> OpsDB
    OpsService --> OpsRedis
    OpsService --> Bakong
```

---

## 👥 Organization & Team Structure

- **Lead & Organization Owner**: [@VibolSen](https://github.com/VibolSen)
- **Development Team ([`@Codebridge404/developers`](https://github.com/orgs/Codebridge404/teams/developers))**:
  - [@kheangsenghorng](https://github.com/kheangsenghorng)
  - [@ChenSreyneat](https://github.com/ChenSreyneat)
  - [@khornSaokhouch](https://github.com/khornSaokhouch)

---

## 🌿 GitFlow & Contribution Guidelines

We enforce a structured, branch-protected development workflow:

```mermaid
gitGraph
   commit id: "Production v1.0"
   branch demo
   checkout demo
   commit id: "Demo / Staging Release"
   branch feature-module
   checkout feature-module
   commit id: "Dev feature work"
   checkout demo
   merge feature-module id: "PR: feature -> demo"
   checkout main
   merge demo id: "Release PR: demo -> master"
```

1. **`master` (Production)**:
   - Protected: Direct pushing and force pushing are blocked.
   - Merges strictly from `demo` via reviewed and approved Pull Requests by Organization Admin (@VibolSen).
2. **`demo` (Staging / Integration)**:
   - Protected: The single source of truth for upcoming releases and team demos.
   - All feature branches must target and merge into `demo` first.
3. **`feature/*` / `fix/*` (Working Branches)**:
   - Branch off `demo`: `git checkout -b feature/your-feature-name`
   - Test locally and push: `git push -u origin feature/your-feature-name`
   - Open Pull Request targeting `demo`.
   - Ensure automated GitHub Actions CI tests pass before review.

---

## 🚀 Quick Setup & Local Development

### 1. Backend Microservices
```bash
git clone https://github.com/Codebridge404/codebridge-services.git
cd codebridge-services

# Start the Docker microservices stack
docker compose up -d --build
```
- API Gateway: `http://localhost:8000`
- Auth Service: `http://localhost:8001`
- Operations Service: `http://localhost:8002`

### 2. Frontend Client
```bash
git clone https://github.com/Codebridge404/codebridgesfront.git
cd codebridgesfront

npm install
npm run dev
```
- Web Application & POS: `http://localhost:3000`

---

<div align="center">
  <sub>© 2026 Codebridge404. Built with precision for modern commerce.</sub>
</div>