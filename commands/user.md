---
description: 👤 Generate User Journey/User Flow Diagram
allowed-tools: Read, Write, Edit, Bash
---

# 👤 User Flow Generator

สร้าง Flowchart แสดง User Journey และ User Experience Flow

## 📋 ขั้นตอน

### 1. ค้นหา User Interactions
```bash
# 1. อ่าน Documentation เกี่ยวกับ User Flow ก่อน!
# ⚠️ ข้าม blog, content, posts - ไม่ใช่ docs ของโปรเจกต์
find . -maxdepth 3 -name "*.md" \
  ! -path "*/blog/*" ! -path "*/posts/*" ! -path "*/content/*" \
  ! -path "*/articles/*" ! -path "*/_posts/*" ! -path "*/news/*" \
  | xargs grep -l -i "user\|flow\|journey\|feature\|guide" 2>/dev/null | head -5

cat README.md docs/USER_GUIDE.md docs/FEATURES.md 2>/dev/null | head -100

# 2. หา routes/pages
find . \( -name "*page*" -o -name "*view*" -o -name "*screen*" -o -name "*component*" \) \
  ! -path "*/node_modules/*" ! -path "*/dist/*" | head -30

# 3. หา forms/actions
grep -r "onSubmit\|handleClick\|@click\|onClick\|handleSubmit" \
  --include="*.jsx" --include="*.tsx" --include="*.vue" --include="*.js" \
  -l 2>/dev/null | head -20

# 4. หา auth flows
find . \( -name "*login*" -o -name "*register*" -o -name "*auth*" -o -name "*signup*" \) \
  ! -path "*/node_modules/*" | head -20

# 5. หา UI states
grep -r "loading\|isLoading\|error\|success\|pending\|useState" \
  --include="*.jsx" --include="*.tsx" --include="*.vue" \
  -l 2>/dev/null | head -10
```

### 2. สร้างไฟล์ `USER_FLOW.md`

```markdown
# 👤 User Flow Diagrams

> 📅 Generated: [วันที่]  
> 📁 Project: [ชื่อ]

---

## 🎯 User Journey Overview

```mermaid
flowchart LR
    subgraph DISCOVER["🔍 Discover"]
        A1["🌐 Landing"]
        A2["📱 Social"]
        A3["🔎 Search"]
    end

    subgraph ENGAGE["💫 Engage"]
        B1["📝 Sign Up"]
        B2["🔐 Login"]
        B3["👀 Browse"]
    end

    subgraph CONVERT["💰 Convert"]
        C1["🛒 Cart"]
        C2["💳 Pay"]
        C3["✅ Done"]
    end

    subgraph RETAIN["🔄 Retain"]
        D1["📧 Email"]
        D2["🔔 Push"]
        D3["🎁 Rewards"]
    end

    DISCOVER --> ENGAGE --> CONVERT --> RETAIN
    RETAIN -.->|"Re-engage"| ENGAGE

    style DISCOVER fill:#e3f2fd
    style ENGAGE fill:#fff3e0
    style CONVERT fill:#e8f5e9
    style RETAIN fill:#f3e5f5
```

---

## 🔐 Registration Flow

```mermaid
flowchart TD
    START["🚀 Start"] --> A["📧 Email"]
    A --> B{"✅ Valid?"}
    
    B -->|"❌"| C["⚠️ Error"]
    C --> A
    
    B -->|"✅"| D["🔑 Password"]
    D --> E{"🔒 Strong?"}
    
    E -->|"❌"| F["💪 Hint"]
    F --> D
    
    E -->|"✅"| G["👤 Profile"]
    G --> H["📨 Verify"]
    H --> I{"✅ OK?"}
    
    I -->|"❌"| J["🔄 Resend"]
    J --> H
    
    I -->|"✅"| K["🎉 Welcome!"]

    style START fill:#e3f2fd
    style K fill:#c8e6c9
    style C fill:#ffcdd2
```

---

## 🔐 Login Flow

```mermaid
flowchart TD
    A["🚀 Login"] --> B["📧 Credentials"]
    B --> C{"🔐 Valid?"}
    
    C -->|"❌"| D["❌ Error"]
    D --> E{"🔢 < 3?"}
    E -->|"✅"| B
    E -->|"❌"| F["🔒 Locked"]
    
    C -->|"✅"| G{"🔐 2FA?"}
    G -->|"❌"| H["🏠 Dashboard"]
    G -->|"✅"| I["📱 Code"]
    
    I --> J{"✅ OK?"}
    J -->|"✅"| H
    J -->|"❌"| K["❌ Retry"]
    K --> I

    style A fill:#e3f2fd
    style H fill:#c8e6c9
    style D fill:#ffcdd2
    style F fill:#ffcdd2
```

---

## 🛒 E-Commerce Flow

```mermaid
flowchart TD
    A["🏠 Home"] --> B["🔍 Browse"]
    B --> C["📦 Product"]
    C --> D{"❤️ Action?"}
    
    D -->|"💾"| E["Wishlist"]
    D -->|"🛒"| F["Add Cart"]
    
    F --> G{"🛒 More?"}
    G -->|"✅"| B
    G -->|"💳"| H["Review"]
    
    H --> I["📍 Address"]
    I --> J["💳 Payment"]
    J --> K{"✅ OK?"}
    
    K -->|"❌"| L["❌ Retry"]
    L --> J
    
    K -->|"✅"| M["📧 Confirm"]
    M --> N["📦 Track"]

    style A fill:#e3f2fd
    style M fill:#c8e6c9
    style N fill:#c8e6c9
    style L fill:#ffcdd2
```

---

## 📝 Form Flow (Generic)

```mermaid
flowchart TD
    A["📝 Open"] --> B["✏️ Fill"]
    B --> C["📤 Submit"]
    C --> D["⏳ Loading"]
    D --> E{"✅ OK?"}
    
    E -->|"✅"| F["🎉 Success"]
    E -->|"⚠️ Validation"| G["Fix Errors"]
    E -->|"❌ Server"| H["🔄 Retry"]
    
    G --> B
    H --> C
    F --> I["➡️ Next"]

    style A fill:#e3f2fd
    style F fill:#c8e6c9
    style G fill:#fff9c4
    style H fill:#ffcdd2
```

---

## 📊 User State Diagram

```mermaid
stateDiagram-v2
    [*] --> Guest
    
    Guest --> Registering: Sign Up
    Guest --> LoggingIn: Login
    
    Registering --> Pending: Submit
    Pending --> Active: Verify ✅
    Pending --> Registering: Resend
    
    LoggingIn --> Active: Success ✅
    LoggingIn --> Guest: Fail ❌
    
    Active --> Guest: Logout
    Active --> Suspended: Violation
    Suspended --> Active: Appeal ✅
    
    Active --> [*]: Delete
    Suspended --> [*]: Delete
```

---

## 🎨 Component State Flow

```mermaid
flowchart LR
    IDLE["😴 Idle"]
    LOADING["⏳ Loading"]
    SUCCESS["✅ Success"]
    ERROR["❌ Error"]
    EMPTY["📭 Empty"]

    IDLE -->|"fetch()"| LOADING
    LOADING -->|"data ✅"| SUCCESS
    LOADING -->|"no data"| EMPTY
    LOADING -->|"fail ❌"| ERROR
    ERROR -->|"retry"| LOADING
    SUCCESS -->|"refresh"| LOADING
    EMPTY -->|"retry"| LOADING

    style IDLE fill:#e3f2fd
    style LOADING fill:#fff9c4
    style SUCCESS fill:#c8e6c9
    style ERROR fill:#ffcdd2
    style EMPTY fill:#f5f5f5
```

---

## 📱 Page Navigation

```mermaid
flowchart TB
    subgraph PUBLIC["🌐 Public"]
        HOME["🏠 Home"]
        LOGIN["🔐 Login"]
        REGISTER["📝 Register"]
    end

    subgraph PROTECTED["🔒 Protected"]
        DASH["📊 Dashboard"]
        PROFILE["👤 Profile"]
        SETTINGS["⚙️ Settings"]
    end

    HOME --> LOGIN & REGISTER
    LOGIN & REGISTER --> DASH
    DASH <--> PROFILE <--> SETTINGS

    style PUBLIC fill:#e3f2fd
    style PROTECTED fill:#e8f5e9
```
```

---

## 🎨 Color Guide

| State | Color | Hex |
|-------|-------|-----|
| 🔵 Start/Input | Light Blue | `#e3f2fd` |
| 🟢 Success | Light Green | `#c8e6c9` |
| 🔴 Error | Light Red | `#ffcdd2` |
| 🟡 Warning | Light Yellow | `#fff9c4` |
| 🟣 Special | Light Purple | `#f3e5f5` |
| ⚪ Neutral | Light Gray | `#f5f5f5` |

เริ่มสร้าง User Flow ได้เลย! 🚀
