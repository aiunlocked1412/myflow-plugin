# 🔄 My Flow - Project Analysis

> 📅 Generated: December 24, 2025
> 📁 Project: myflow-plugin
> 🛠️ Stack: Claude Code Plugin (Markdown-based)

---

## 📊 Project Overview

| รายการ | รายละเอียด |
|--------|------------|
| **ประเภท** | Claude Code Plugin |
| **ภาษาหลัก** | Markdown (Command Templates) |
| **Framework** | Claude Code Plugin System |
| **Architecture** | Command-based Plugin |
| **Version** | 1.0.1 |
| **License** | MIT |

---

## 🏗️ System Architecture Flow

```mermaid
flowchart TB
    subgraph USER["👤 User Layer"]
        CLI["⌨️ Claude Code CLI"]
        CMD["📝 User Command<br/>/myflow, /myflow:er, etc."]
    end

    subgraph PLUGIN["🔌 Plugin Layer"]
        MANIFEST["📋 Marketplace.json<br/>Plugin Registration"]

        subgraph COMMANDS["📁 Commands"]
            direction LR
            MYFLOW["🔍 myflow.md<br/>Full Analysis"]
            UPDATE["🔄 update.md<br/>Incremental"]
            SYSTEM["🏗️ system.md<br/>Architecture"]
            DATA["📊 data.md<br/>Data Flow"]
            ER["🗄️ er.md<br/>ER Diagram"]
            USERFLOW["👤 user.md<br/>User Flow"]
        end

        subgraph SKILLS["🎯 Skills"]
            FLOW_SKILL["📄 flow-analysis/SKILL.md<br/>Auto-trigger Analysis"]
        end
    end

    subgraph OUTPUT["📤 Output Layer"]
        direction LR
        ANALYSIS["📄 MY_FLOW_ANALYSIS.md"]
        SYSTEM_OUT["📄 SYSTEM_FLOW.md"]
        DATA_OUT["📄 DATA_FLOW.md"]
        ER_OUT["📄 ER_DIAGRAM.md"]
        USER_OUT["📄 USER_FLOW.md"]
        UPDATE_OUT["📄 MY_FLOW_UPDATE.md"]
    end

    USER --> PLUGIN
    CLI --> MANIFEST
    CMD --> COMMANDS
    COMMANDS --> OUTPUT
    SKILLS -.->|"Auto-invoke"| COMMANDS

    style USER fill:#e3f2fd,stroke:#1976d2
    style PLUGIN fill:#fff3e0,stroke:#f57c00
    style COMMANDS fill:#f3e5f5,stroke:#7b1fa2
    style SKILLS fill:#e8f5e9,stroke:#388e3c
    style OUTPUT fill:#c8e6c9,stroke:#4caf50
```

---

## 🔄 Plugin Execution Flow

```mermaid
flowchart TD
    A["🚀 User types /myflow"] --> B["🔌 Claude Code loads Plugin"]
    B --> C["📋 Read marketplace.json"]
    C --> D["📁 Find matching command"]
    D --> E{"🔍 Command found?"}

    E -->|"✅ Yes"| F["📄 Load command .md file"]
    E -->|"❌ No"| G["❌ Show error"]

    F --> H["🤖 Claude executes prompt"]
    H --> I["🔍 Analyze codebase"]
    I --> J["📊 Generate Mermaid diagrams"]
    J --> K["📝 Create output .md file"]
    K --> L["✅ Done"]

    style A fill:#e3f2fd
    style L fill:#c8e6c9
    style G fill:#ffcdd2
```

---

## 📦 Key Components

### 📋 Configuration Files
| ไฟล์ | Path | หน้าที่ |
|------|------|--------|
| marketplace.json | `.claude-plugin/marketplace.json` | Plugin manifest สำหรับ Claude Code Marketplace |

### 📁 Commands
| ไฟล์ | Command | หน้าที่ |
|------|---------|--------|
| myflow.md | `/myflow` | วิเคราะห์โปรเจกต์แบบครบวงจร (Default) |
| update.md | `/myflow:update` | อัพเดทเฉพาะส่วนที่เปลี่ยนแปลง |
| system.md | `/myflow:system` | สร้าง System Architecture Flowchart |
| data.md | `/myflow:data` | สร้าง Data Flow Diagram |
| er.md | `/myflow:er` | สร้าง ER Diagram |
| user.md | `/myflow:user` | สร้าง User Journey/User Flow |

### 🎯 Skills
| ไฟล์ | Path | หน้าที่ |
|------|------|--------|
| SKILL.md | `skills/flow-analysis/SKILL.md` | Auto-trigger เมื่อผู้ใช้ต้องการวิเคราะห์โปรเจกต์ |

---

## 🗄️ Plugin Structure (ER-style)

```mermaid
erDiagram
    MARKETPLACE_JSON ||--|{ PLUGIN : "contains"
    MARKETPLACE_JSON {
        string schema "JSON Schema URL"
        string name "myflow-marketplace"
        string version "1.0.1"
        object owner "AI Unlocked"
    }

    PLUGIN ||--|{ COMMAND : "has"
    PLUGIN {
        string name "myflow"
        string description "Generate Flowcharts"
        string version "1.0.1"
        string source "./"
        string category "productivity"
    }

    COMMAND {
        string filename "*.md"
        string description "Command description"
        array allowed_tools "Read, Write, Edit, Bash"
        text prompt_template "Instructions"
    }

    PLUGIN ||--o| SKILL : "may have"
    SKILL {
        string name "flow-analysis"
        string description "Auto-trigger"
        array triggers "keywords"
        text instructions "Skill prompt"
    }
```

---

## 📊 Data Flow

```mermaid
flowchart LR
    subgraph INPUT["📥 Input Sources"]
        USER_CMD["👤 User Command"]
        CODEBASE["📁 Target Codebase"]
        DOCS["📄 README/Docs"]
    end

    subgraph PROCESS["⚙️ Processing"]
        direction TB
        DISCOVER["🔍 Discover Files"]
        ANALYZE["📊 Analyze Structure"]
        GENERATE["🎨 Generate Diagrams"]
    end

    subgraph OUTPUT["📤 Output"]
        MD_FILE["📄 Markdown Files"]
        MERMAID["📊 Mermaid Diagrams"]
        TABLES["📋 Summary Tables"]
    end

    USER_CMD --> DISCOVER
    CODEBASE --> DISCOVER
    DOCS --> ANALYZE
    DISCOVER --> ANALYZE --> GENERATE
    GENERATE --> MD_FILE & MERMAID & TABLES

    style INPUT fill:#e3f2fd
    style PROCESS fill:#fff9c4
    style OUTPUT fill:#c8e6c9
```

---

## 👤 User Flow

```mermaid
flowchart TD
    START["🚀 Start"] --> A{"🔍 What to analyze?"}

    A -->|"Full Analysis"| B["/myflow"]
    A -->|"System Only"| C["/myflow:system"]
    A -->|"Data Flow"| D["/myflow:data"]
    A -->|"ER Diagram"| E["/myflow:er"]
    A -->|"User Flow"| F["/myflow:user"]
    A -->|"Changes Only"| G["/myflow:update"]

    B --> H["📄 MY_FLOW_ANALYSIS.md"]
    C --> I["📄 SYSTEM_FLOW.md"]
    D --> J["📄 DATA_FLOW.md"]
    E --> K["📄 ER_DIAGRAM.md"]
    F --> L["📄 USER_FLOW.md"]
    G --> M["📄 MY_FLOW_UPDATE.md"]

    H & I & J & K & L & M --> N["✅ Review Output"]
    N --> O{"🔄 Need more?"}
    O -->|"Yes"| A
    O -->|"No"| P["🎉 Done"]

    style START fill:#e3f2fd
    style P fill:#c8e6c9
```

---

## 🔗 Command Dependencies

```mermaid
flowchart TB
    subgraph CORE["🔍 Core Commands"]
        MAIN["myflow.md<br/>Full Analysis"]
    end

    subgraph SPECIALIZED["🎯 Specialized"]
        direction LR
        SYS["system.md"]
        DAT["data.md"]
        ERD["er.md"]
        USR["user.md"]
    end

    subgraph UTILITY["🔧 Utility"]
        UPD["update.md<br/>Incremental"]
    end

    MAIN -->|"includes patterns from"| SYS & DAT & ERD & USR
    UPD -->|"references"| MAIN

    style CORE fill:#f3e5f5,stroke:#7b1fa2
    style SPECIALIZED fill:#e3f2fd,stroke:#1976d2
    style UTILITY fill:#fff3e0,stroke:#f57c00
```

---

## 🔧 Supported Frameworks Detection

```mermaid
flowchart LR
    subgraph DETECT["🔍 Detection"]
        direction TB
        FILES["📁 Find Files"]
        CONFIG["📋 Check Config"]
    end

    subgraph PYTHON["🐍 Python"]
        DJANGO["Django"]
        FASTAPI["FastAPI"]
        FLASK["Flask"]
        SQLALCHEMY["SQLAlchemy"]
    end

    subgraph JS_TS["🟨 JavaScript/TypeScript"]
        EXPRESS["Express"]
        NEST["NestJS"]
        NEXT["Next.js"]
        PRISMA["Prisma"]
        TYPEORM["TypeORM"]
    end

    subgraph RUST["🦀 Rust"]
        ACTIX["Actix"]
        AXUM["Axum"]
        DIESEL["Diesel"]
        SEAORM["SeaORM"]
    end

    subgraph GO["🔵 Go"]
        GIN["Gin"]
        ECHO["Echo"]
        GORM["GORM"]
    end

    DETECT --> PYTHON & JS_TS & RUST & GO

    style DETECT fill:#fff9c4
    style PYTHON fill:#3572A5,color:white
    style JS_TS fill:#f7df1e
    style RUST fill:#dea584
    style GO fill:#00ADD8,color:white
```

---

## 📋 Output File Specifications

| Output File | Command | Content |
|-------------|---------|---------|
| `MY_FLOW_ANALYSIS.md` | `/myflow` | Complete analysis with all diagrams |
| `SYSTEM_FLOW.md` | `/myflow:system` | System architecture, request flow, service communication |
| `DATA_FLOW.md` | `/myflow:data` | Data sources, processing, storage, CRUD flows |
| `ER_DIAGRAM.md` | `/myflow:er` | Entity relationships, table details, indexes |
| `USER_FLOW.md` | `/myflow:user` | User journeys, registration, login, navigation |
| `MY_FLOW_UPDATE.md` | `/myflow:update` | Changes since last analysis, changelogs |

---

## 💡 Notes & Recommendations

### 👍 Strengths
1. **Modular Commands** - แยก command เป็นไฟล์ ทำให้ maintain ง่าย
2. **Comprehensive Templates** - มี template พร้อมใช้สำหรับทุกประเภท diagram
3. **Multi-framework Support** - รองรับหลายภาษาและ framework
4. **Incremental Update** - มี `/myflow:update` สำหรับอัพเดทเฉพาะส่วนที่เปลี่ยน
5. **Bilingual Documentation** - README มีทั้งภาษาไทยและอังกฤษ

### 📝 Future Enhancements
1. เพิ่ม command สำหรับ Sequence Diagram
2. เพิ่ม Class Diagram generator
3. รองรับ C#/.NET และ Ruby on Rails เพิ่มเติม
4. เพิ่ม API documentation generator

---

## 🔒 Security Considerations

- Plugin ใช้เฉพาะ `Read, Write, Edit, Bash` tools
- ไม่มีการส่งข้อมูลออกนอกระบบ
- Output files สร้างใน directory ของโปรเจกต์เท่านั้น

---

Made with ❤️ by **AI Unlocked** | Version 1.0.1
