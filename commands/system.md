---
description: 🏗️ สร้าง System Architecture Flowchart
allowed-tools: Read, Write, Edit, Bash
---

# 🏗️ System Architecture Flow Generator

สร้าง Flowchart แสดงโครงสร้างระบบทั้งหมด

## 📋 ขั้นตอน

### 1. ค้นหา Components
```bash
# 1. อ่าน Documentation ก่อน!
# ⚠️ ข้าม blog, content, posts - ไม่ใช่ docs ของโปรเจกต์
find . -maxdepth 3 -name "*.md" \
  ! -path "*/blog/*" ! -path "*/posts/*" ! -path "*/content/*" \
  ! -path "*/articles/*" ! -path "*/_posts/*" ! -path "*/news/*" \
  | xargs grep -l -i "architect\|system\|overview\|structure" 2>/dev/null | head -5
  
cat README.md ARCHITECTURE.md docs/SYSTEM.md docs/OVERVIEW.md 2>/dev/null | head -100

# 2. Entry points
find . \( -name "main.*" -o -name "app.*" -o -name "index.*" -o -name "server.*" \) \
  ! -path "*/node_modules/*" ! -path "*/dist/*" | head -10

# 3. Routes & Controllers
find . \( -name "*route*" -o -name "*controller*" -o -name "*handler*" \) \
  ! -path "*/node_modules/*" | head -20

# 4. Services & Repositories
find . \( -name "*service*" -o -name "*repository*" -o -name "*usecase*" \) \
  ! -path "*/node_modules/*" | head -20

# 5. Config & Infrastructure
find . \( -name "*.env*" -o -name "*config*" -o -name "docker-compose*" -o -name "Dockerfile" \) \
  ! -path "*/node_modules/*" | head -10
cat docker-compose.yml docker-compose.yaml 2>/dev/null | head -50
```

### 2. สร้างไฟล์ `SYSTEM_FLOW.md`

```markdown
# 🏗️ System Architecture Flow

> 📅 Generated: [วันที่]  
> 📁 Project: [ชื่อ]

---

## 🎯 High-Level Architecture

```mermaid
flowchart TB
    subgraph CLIENTS["🖥️ Clients"]
        direction LR
        WEB["🌐 Web<br/>React/Vue/Angular"]
        MOBILE["📱 Mobile<br/>iOS/Android"]
        THIRD["🔌 Third Party<br/>Partners"]
    end

    subgraph GATEWAY["🚪 Gateway Layer"]
        LB["⚖️ Load Balancer"]
        CDN["🌍 CDN"]
        WAF["🛡️ WAF"]
    end

    subgraph API["⚡ API Layer"]
        direction LR
        GW["🚪 API Gateway"]
        AUTH["🔐 Auth Service"]
        RATE["⏱️ Rate Limiter"]
    end

    subgraph SERVICES["⚙️ Microservices"]
        direction TB
        USER["👤 User Service"]
        ORDER["🛒 Order Service"]
        PAYMENT["💳 Payment Service"]
        NOTIFY["🔔 Notification"]
    end

    subgraph DATA["💾 Data Layer"]
        direction LR
        DB[("🗄️ PostgreSQL")]
        REDIS[("⚡ Redis")]
        S3["☁️ S3 Storage"]
        KAFKA["📨 Kafka"]
    end

    subgraph EXTERNAL["🌐 External"]
        STRIPE["💳 Stripe"]
        SENDGRID["📧 SendGrid"]
        TWILIO["📱 Twilio"]
    end

    CLIENTS --> GATEWAY
    GATEWAY --> API
    API --> SERVICES
    SERVICES --> DATA
    SERVICES --> EXTERNAL

    style CLIENTS fill:#e3f2fd,stroke:#1976d2
    style GATEWAY fill:#fce4ec,stroke:#c2185b
    style API fill:#fff3e0,stroke:#f57c00
    style SERVICES fill:#f3e5f5,stroke:#7b1fa2
    style DATA fill:#e8f5e9,stroke:#388e3c
    style EXTERNAL fill:#fff8e1,stroke:#fbc02d
```

---

## 🔄 Request Flow

```mermaid
flowchart LR
    A["📱 Client"] --> B["⚖️ Load Balancer"]
    B --> C["🚪 API Gateway"]
    C --> D{"🔐 Auth?"}
    
    D -->|"✅ Valid"| E["🛤️ Router"]
    D -->|"❌ Invalid"| F["🚫 401 Error"]
    
    E --> G["⚙️ Service"]
    G --> H["💾 Database"]
    H --> G
    G --> I["📬 Response"]
    
    style A fill:#e3f2fd
    style I fill:#c8e6c9
    style F fill:#ffcdd2
```

---

## 📦 Service Communication

```mermaid
flowchart TB
    subgraph SYNC["🔄 Synchronous"]
        A["Service A"] -->|"REST/gRPC"| B["Service B"]
    end

    subgraph ASYNC["📨 Asynchronous"]
        C["Service C"] -->|"Publish"| Q[["📨 Message Queue"]]
        Q -->|"Subscribe"| D["Service D"]
        Q -->|"Subscribe"| E["Service E"]
    end

    style SYNC fill:#e3f2fd
    style ASYNC fill:#fff3e0
```

---

## 🗂️ Layer Details

### Gateway Layer
| Component | Technology | Purpose |
|-----------|------------|---------|
| Load Balancer | Nginx/ALB | จัดการ traffic |
| CDN | CloudFront | Cache static files |
| WAF | AWS WAF | Security |

### Service Layer
| Service | Port | Responsibility |
|---------|------|----------------|
| ... | ... | ... |

### Data Layer
| Store | Type | Usage |
|-------|------|-------|
| ... | ... | ... |

---

## 🔗 Integration Points

```mermaid
flowchart LR
    subgraph INTERNAL["🏠 Internal"]
        SVC["⚙️ Our Services"]
    end

    subgraph EXTERNAL["🌐 External APIs"]
        PAY["💳 Payment Gateway"]
        EMAIL["📧 Email Service"]
        SMS["📱 SMS Gateway"]
        MAP["🗺️ Maps API"]
    end

    SVC <-->|"HTTPS"| PAY
    SVC -->|"SMTP/API"| EMAIL
    SVC -->|"API"| SMS
    SVC -->|"API"| MAP

    style INTERNAL fill:#e8f5e9
    style EXTERNAL fill:#fff8e1
```
```

---

## 🎨 Style Guide

ใช้สีตาม Layer:
- 🔵 Client: `#e3f2fd`
- 🟠 API: `#fff3e0`  
- 🟣 Service: `#f3e5f5`
- 🟢 Data: `#e8f5e9`
- 🟡 External: `#fff8e1`
- 🔴 Error: `#ffcdd2`
- 🟢 Success: `#c8e6c9`

เริ่มสร้าง System Flow ได้เลย! 🚀
