---
description: 📊 Generate Data Flow Diagram
allowed-tools: Read, Write, Edit, Bash
---

# 📊 Data Flow Generator

สร้าง Flowchart แสดงการไหลของข้อมูลในระบบ

## 📋 ขั้นตอน

### 1. ค้นหา Data Sources & Sinks
```bash
# 1. อ่าน Documentation ก่อน!
# ⚠️ ข้าม blog, content, posts
find . -maxdepth 3 -name "*.md" \
  ! -path "*/blog/*" ! -path "*/posts/*" ! -path "*/content/*" \
  ! -path "*/articles/*" ! -path "*/_posts/*" \
  | xargs grep -l -i "data\|api\|integration\|flow" 2>/dev/null | head -5

# 2. หา API endpoints
find . \( -name "*api*" -o -name "*route*" -o -name "*endpoint*" \) \
  ! -path "*/node_modules/*" | head -20

# 3. หา Services & Repositories
find . \( -name "*service*" -o -name "*repository*" -o -name "*dao*" \) \
  ! -path "*/node_modules/*" | head -20

# 4. หา External integrations
grep -r "axios\|fetch\|http\|request\|api" \
  --include="*.js" --include="*.ts" --include="*.py" \
  -l 2>/dev/null | head -20

# 5. หา Message Queue / Events
find . \( -name "*queue*" -o -name "*event*" -o -name "*kafka*" -o -name "*rabbit*" \) \
  ! -path "*/node_modules/*" | head -10

# 6. หา Cache config
grep -r "redis\|cache\|memcache" \
  --include="*.js" --include="*.ts" --include="*.py" --include="*.yaml" \
  -l 2>/dev/null | head -10
```

### 2. สร้างไฟล์ `DATA_FLOW.md`

```markdown
# 📊 Data Flow Diagrams

> 📅 Generated: [วันที่]  
> 📁 Project: [ชื่อ]

---

## 🎯 High-Level Data Flow

```mermaid
flowchart LR
    subgraph SOURCES["📥 Data Sources"]
        U["👤 User Input"]
        API["🌐 External API"]
        FILE["📁 File Upload"]
        WH["🔔 Webhook"]
    end

    subgraph INGESTION["🚪 Ingestion"]
        VAL["✅ Validate"]
        PARSE["📝 Parse"]
        NORM["🔄 Normalize"]
    end

    subgraph PROCESS["⚙️ Processing"]
        BIZ["📦 Business Logic"]
        TRANS["🔄 Transform"]
        ENRICH["✨ Enrich"]
    end

    subgraph STORAGE["💾 Storage"]
        DB[("🗄️ Database")]
        CACHE[("⚡ Cache")]
        S3["☁️ Object Store"]
        SEARCH["🔍 Search Index"]
    end

    subgraph OUTPUT["📤 Output"]
        RES["📬 API Response"]
        EMAIL["📧 Email"]
        PUSH["🔔 Push"]
        REPORT["📊 Report"]
    end

    SOURCES --> INGESTION
    INGESTION --> PROCESS
    PROCESS --> STORAGE
    STORAGE --> OUTPUT

    style SOURCES fill:#e3f2fd
    style INGESTION fill:#fff3e0
    style PROCESS fill:#f3e5f5
    style STORAGE fill:#e8f5e9
    style OUTPUT fill:#fce4ec
```

---

## 📥 Data Input Flow

```mermaid
flowchart TD
    subgraph INPUT["📥 Input Sources"]
        REST["🌐 REST API"]
        GQL["📊 GraphQL"]
        WS["🔌 WebSocket"]
        FORM["📝 Form"]
    end

    subgraph VALIDATE["✅ Validation Layer"]
        SCHEMA["📋 Schema Validate"]
        SANITIZE["🧹 Sanitize"]
        AUTH_CHECK["🔐 Auth Check"]
    end

    subgraph TRANSFORM["🔄 Transform"]
        DTO["📦 DTO Mapping"]
        ENRICH["✨ Enrich Data"]
    end

    INPUT --> VALIDATE
    VALIDATE -->|"✅ Valid"| TRANSFORM
    VALIDATE -->|"❌ Invalid"| ERR["⚠️ Error Response"]

    style INPUT fill:#e3f2fd
    style VALIDATE fill:#fff9c4
    style TRANSFORM fill:#e8f5e9
    style ERR fill:#ffcdd2
```

---

## 💾 Database Operations Flow

```mermaid
flowchart LR
    subgraph APP["⚙️ Application"]
        SVC["Service"]
        REPO["Repository"]
    end

    subgraph CACHE["⚡ Cache Layer"]
        CHECK{"Cache Hit?"}
        GET["Get Cache"]
        SET["Set Cache"]
    end

    subgraph DB["🗄️ Database"]
        READ["📖 Read"]
        WRITE["✏️ Write"]
    end

    SVC --> REPO
    REPO --> CHECK
    CHECK -->|"✅ Hit"| GET --> SVC
    CHECK -->|"❌ Miss"| READ --> SET --> SVC
    
    REPO -->|"Write"| WRITE --> SET

    style APP fill:#f3e5f5
    style CACHE fill:#fff3e0
    style DB fill:#e8f5e9
```

---

## 🔄 Event-Driven Flow

```mermaid
flowchart TB
    subgraph PRODUCER["📤 Producers"]
        API_P["🌐 API"]
        CRON["⏰ Scheduler"]
        WH_P["🔔 Webhook"]
    end

    subgraph QUEUE["📨 Message Queue"]
        Q[["Kafka/RabbitMQ"]]
    end

    subgraph CONSUMER["📥 Consumers"]
        EMAIL_C["📧 Email Worker"]
        NOTIFY_C["🔔 Notification"]
        ANALYTICS["📊 Analytics"]
        SYNC["🔄 Data Sync"]
    end

    PRODUCER -->|"Publish"| Q
    Q -->|"Subscribe"| CONSUMER

    style PRODUCER fill:#e3f2fd
    style QUEUE fill:#fff3e0
    style CONSUMER fill:#e8f5e9
```

---

## 🔁 CRUD Data Flow

### Create Flow
```mermaid
flowchart LR
    A["📝 Input"] --> B["✅ Validate"]
    B --> C["🔄 Transform"]
    C --> D["💾 Save DB"]
    D --> E["⚡ Update Cache"]
    E --> F["📤 Response"]

    style A fill:#e3f2fd
    style F fill:#c8e6c9
```

### Read Flow
```mermaid
flowchart LR
    A["📥 Request"] --> B{"⚡ Cache?"}
    B -->|"Hit"| C["Return Cache"]
    B -->|"Miss"| D["📖 Query DB"]
    D --> E["⚡ Set Cache"]
    E --> F["📤 Response"]
    C --> F

    style A fill:#e3f2fd
    style F fill:#c8e6c9
```

### Update Flow
```mermaid
flowchart LR
    A["📝 Input"] --> B["✅ Validate"]
    B --> C["💾 Update DB"]
    C --> D["🗑️ Invalidate Cache"]
    D --> E["📤 Response"]

    style A fill:#e3f2fd
    style E fill:#c8e6c9
```

### Delete Flow
```mermaid
flowchart LR
    A["🗑️ Request"] --> B["🔐 Auth Check"]
    B --> C["💾 Delete DB"]
    C --> D["🗑️ Clear Cache"]
    D --> E["📤 Response"]

    style A fill:#e3f2fd
    style E fill:#c8e6c9
```

---

## 🌐 External Integration Flow

```mermaid
flowchart TB
    subgraph INTERNAL["🏠 Our System"]
        SVC["⚙️ Service"]
        ADAPTER["🔌 Adapter"]
        RETRY["🔄 Retry Logic"]
        CIRCUIT["⚡ Circuit Breaker"]
    end

    subgraph EXTERNAL["🌐 External APIs"]
        PAY["💳 Payment"]
        EMAIL["📧 Email"]
        SMS["📱 SMS"]
        MAP["🗺️ Maps"]
    end

    SVC --> ADAPTER
    ADAPTER --> CIRCUIT
    CIRCUIT --> RETRY
    RETRY <-->|"HTTPS"| EXTERNAL

    style INTERNAL fill:#e8f5e9
    style EXTERNAL fill:#fff3e0
```

---

## 📊 Data Flow Summary

| Flow | Source | Process | Destination | Type |
|------|--------|---------|-------------|------|
| User Registration | Form | Validate → Hash → Save | DB + Email | Sync |
| Order Creation | API | Validate → Process → Save | DB + Queue | Sync + Async |
| Payment | Service | Adapter → External API | Payment Gateway | Sync |
| Notification | Queue | Consume → Process → Send | Email/Push | Async |

---

## 🔐 Data Security Flow

```mermaid
flowchart LR
    A["📥 Raw Data"] --> B["🔐 Encrypt"]
    B --> C["💾 Store"]
    C --> D["🔓 Decrypt"]
    D --> E["📤 Output"]

    style A fill:#ffcdd2
    style B fill:#fff9c4
    style C fill:#e8f5e9
    style D fill:#fff9c4
    style E fill:#c8e6c9
```
```

เริ่มสร้าง Data Flow ได้เลย! 🚀
