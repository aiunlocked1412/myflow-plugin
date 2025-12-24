---
description: 🔍 Analyze project, generate Flowcharts + ER Diagram
allowed-tools: Read, Write, Edit, Bash
---

# 🔍 My Flow - Full Project Analysis

คุณคือผู้เชี่ยวชาญด้าน System Design และ Documentation ทำการวิเคราะห์โปรเจกต์แบบครบวงจร

## 📋 ขั้นตอนการทำงาน

### Step 1: สำรวจโปรเจกต์
```bash
# 1. อ่าน Documentation ก่อน (สำคัญมาก!)
# ⚠️ ข้าม blog, content, posts, articles - ไม่ใช่ docs ของโปรเจกต์
find . -maxdepth 3 -type f -name "*.md" \
  ! -path "*/blog/*" ! -path "*/posts/*" ! -path "*/content/*" \
  ! -path "*/articles/*" ! -path "*/_posts/*" ! -path "*/news/*" \
  | head -20
  
# อ่าน README และ docs หลัก
cat README.md 2>/dev/null
cat ARCHITECTURE.md CONTRIBUTING.md docs/README.md 2>/dev/null | head -100

# 2. หาไฟล์ code ทั้งหมด
find . -type f \( -name "*.py" -o -name "*.js" -o -name "*.ts" -o -name "*.tsx" -o -name "*.jsx" -o -name "*.java" -o -name "*.go" -o -name "*.php" -o -name "*.rb" -o -name "*.rs" \) \
  ! -path "*/node_modules/*" ! -path "*/.git/*" ! -path "*/vendor/*" ! -path "*/dist/*" ! -path "*/target/*" \
  | head -100

# 3. หา config files
ls -la package.json requirements.txt go.mod pom.xml composer.json Gemfile Cargo.toml pyproject.toml 2>/dev/null
cat package.json 2>/dev/null | head -50

# 4. หา routes/controllers
find . \( -name "*route*" -o -name "*controller*" -o -name "*handler*" -o -name "*endpoint*" \) \
  ! -path "*/node_modules/*" | head -20

# 5. หา models/schemas
find . \( -name "*model*" -o -name "*entity*" -o -name "*.prisma" -o -name "*schema*" -o -name "*migration*" \) \
  ! -path "*/node_modules/*" | head -20

# 6. หา diagrams ที่มีอยู่แล้ว
find . \( -name "*.mermaid" -o -name "*diagram*" -o -name "*flow*" \) \
  ! -path "*/node_modules/*" | head -10
```

### Step 2: วิเคราะห์และสร้าง Output

สร้างไฟล์ `MY_FLOW_ANALYSIS.md` ตามรูปแบบนี้:

---

```markdown
# 🔄 My Flow - Project Analysis

> 📅 Generated: [วันที่]  
> 📁 Project: [ชื่อโปรเจกต์]  
> 🛠️ Stack: [Tech Stack]

---

## 📊 Project Overview

| รายการ | รายละเอียด |
|--------|------------|
| **ภาษาหลัก** | [ภาษา] |
| **Framework** | [Framework] |
| **Database** | [DB Type] |
| **Architecture** | [Pattern] |

---

## 🏗️ System Architecture Flow

```mermaid
flowchart TB
    subgraph CLIENT["🖥️ Client Layer"]
        WEB["🌐 Web App"]
        MOBILE["📱 Mobile App"]
        CLI["⌨️ CLI"]
    end

    subgraph API["⚡ API Layer"]
        GW["🚪 API Gateway"]
        AUTH["🔐 Auth"]
        ROUTE["🛤️ Router"]
    end

    subgraph SERVICE["⚙️ Service Layer"]
        BIZ["📦 Business Logic"]
        VALID["✅ Validation"]
        TRANS["🔄 Transform"]
    end

    subgraph DATA["💾 Data Layer"]
        DB[("🗄️ Database")]
        CACHE[("⚡ Cache")]
        QUEUE["📨 Queue"]
    end

    CLIENT --> API
    API --> SERVICE
    SERVICE --> DATA

    style CLIENT fill:#e1f5fe
    style API fill:#fff3e0
    style SERVICE fill:#f3e5f5
    style DATA fill:#e8f5e9
```

---

## 🔐 Authentication Flow

```mermaid
flowchart TD
    A["🚀 Start"] --> B{"🔑 มี Token?"}
    
    B -->|"✅ Yes"| C["🔍 Validate Token"]
    B -->|"❌ No"| D["📝 Login Page"]
    
    C --> E{"✅ Valid?"}
    E -->|"✅ Yes"| F["🎉 Access Granted"]
    E -->|"❌ No"| G["🔄 Refresh Token"]
    
    G --> H{"🔄 Refresh OK?"}
    H -->|"✅ Yes"| F
    H -->|"❌ No"| D
    
    D --> I["📧 Enter Credentials"]
    I --> J["🔐 Authenticate"]
    J --> K{"✅ Success?"}
    K -->|"✅ Yes"| L["🎫 Generate Token"]
    K -->|"❌ No"| M["❌ Show Error"]
    M --> D
    
    L --> F

    style F fill:#c8e6c9,stroke:#4caf50
    style M fill:#ffcdd2,stroke:#f44336
```

---

## 🔄 Main Business Flow

```mermaid
flowchart LR
    subgraph INPUT["📥 Input"]
        REQ["📨 Request"]
        FILE["📁 File"]
        EVENT["⚡ Event"]
    end

    subgraph PROCESS["⚙️ Processing"]
        direction TB
        V["✅ Validate"] --> B["📦 Business Logic"]
        B --> T["🔄 Transform"]
    end

    subgraph OUTPUT["📤 Output"]
        RES["📬 Response"]
        NOTIFY["🔔 Notification"]
        LOG["📝 Log"]
    end

    INPUT --> PROCESS
    PROCESS --> OUTPUT

    style INPUT fill:#bbdefb
    style PROCESS fill:#fff9c4
    style OUTPUT fill:#c8e6c9
```

---

## 🗄️ ER Diagram

```mermaid
erDiagram
    USER ||--o{ ORDER : "places"
    USER {
        int id PK "รหัสผู้ใช้"
        string email UK "อีเมล"
        string name "ชื่อ"
        string password "รหัสผ่าน"
        datetime created_at "วันที่สร้าง"
    }
    
    ORDER ||--|{ ORDER_ITEM : "contains"
    ORDER {
        int id PK "รหัสออเดอร์"
        int user_id FK "รหัสผู้ใช้"
        decimal total "ยอดรวม"
        string status "สถานะ"
        datetime created_at "วันที่สั่ง"
    }
    
    PRODUCT ||--o{ ORDER_ITEM : "ordered_in"
    PRODUCT {
        int id PK "รหัสสินค้า"
        string name "ชื่อสินค้า"
        decimal price "ราคา"
        int stock "จำนวนคงเหลือ"
    }
    
    ORDER_ITEM {
        int id PK "รหัสรายการ"
        int order_id FK "รหัสออเดอร์"
        int product_id FK "รหัสสินค้า"
        int quantity "จำนวน"
        decimal price "ราคา"
    }
```

---

## 📊 Data Flow

```mermaid
flowchart LR
    subgraph SOURCE["📊 Data Sources"]
        U["👤 User Input"]
        API["🌐 External API"]
        F["📁 File Upload"]
    end

    subgraph PROCESS["⚙️ Processing"]
        V["✅ Validate"]
        E["🔧 Enrich"]
        T["🔄 Transform"]
    end

    subgraph STORE["💾 Storage"]
        DB[("🗄️ Database")]
        S3["☁️ File Storage"]
        CACHE[("⚡ Cache")]
    end

    U --> V
    API --> V
    F --> V
    V --> E --> T
    T --> DB & S3 & CACHE

    style SOURCE fill:#e3f2fd
    style PROCESS fill:#fff8e1
    style STORE fill:#e8f5e9
```

---

## 📦 Key Components

### Controllers/Handlers
| ชื่อ | Path | หน้าที่ |
|------|------|--------|
| ... | ... | ... |

### Services
| ชื่อ | Path | หน้าที่ |
|------|------|--------|
| ... | ... | ... |

### Models
| ชื่อ | Path | หน้าที่ |
|------|------|--------|
| ... | ... | ... |

---

## 🔗 API Endpoints

| Method | Endpoint | Flow | Description |
|--------|----------|------|-------------|
| POST | /auth/login | Auth Flow | เข้าสู่ระบบ |
| GET | /users | User Flow | ดึงข้อมูลผู้ใช้ |
| POST | /orders | Order Flow | สร้างออเดอร์ |

---

## 💡 Notes & Recommendations

[ข้อเสนอแนะ]
```

---

## ⚠️ กฎสำคัญ

1. **Mermaid ต้อง Render ได้** - ตรวจสอบ syntax ก่อนส่ง
2. **ใช้ Emoji** ทำให้อ่านง่ายและสวยงาม
3. **ใช้สี** แยก subgraph ด้วย `style`
4. **ครอบคลุมทุก Flow** ที่พบในโปรเจกต์
5. **ภาษาไทย** ในคำอธิบาย, อังกฤษใน diagram

เริ่มวิเคราะห์โปรเจกต์ได้เลย! 🚀
