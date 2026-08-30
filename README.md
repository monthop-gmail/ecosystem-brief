# ecosystem-brief

> **Start here.** แผนที่กลางของ Monthop AI Ecosystem — สำหรับทั้งคนและ AI

repo นี้ **ไม่ใช่** implementation และ **ไม่ใช่** source of truth
มันคือ **Map of Truth** — บอกว่า ecosystem เรามีอะไร อยู่ชั้นไหน repo ไหนเป็นเจ้าของ และถ้าจะทำของใหม่ควรไปแก้ตรงไหน

**เป้าหมาย: เปิดอ่าน 1 นาทีแล้วเห็นภาพเดียวกัน**

| ต้องการ | ไปที่ |
|---|---|
| 🤖 **เป็น AI agent กำลังจะแก้ repo** | **[`ai/context.md`](ai/context.md) — อ่านก่อนเสมอ** |
| 🔍 หาว่าใครเป็นเจ้าของความสามารถหนึ่ง | [Capability Index](docs/repositories.md#capability-index) |
| 🗺️ เพิ่งเข้าทีม อยากเห็นภาพรวม | [`docs/ecosystem.md`](docs/ecosystem.md) |
| 🏗️ อยากเห็น architecture + boundary | [`docs/architecture.md`](docs/architecture.md) |
| 📋 หา repo ตาม layer | [`docs/repositories.md`](docs/repositories.md) |

---

## แต่ละ repo ทำหน้าที่อะไรใน ecosystem

```text
        ecosystem-brief          "สมองส่วนแผนที่"   — ควรเป็นอะไร
               │
        ecosystem-intelligence   "ตา"               — ตอนนี้เป็นอะไรจริง
               │
        agent-platform           "ระบบกลาง"          — contract และ runtime
               │
        devfactory-core          "มือที่ลงมือทำ"      — ส่งมอบและ orchestrate
```

`ecosystem-brief` **ไม่ควรพยายามกลายเป็นตัวควบคุม ecosystem** — มันมีหน้าที่ชี้ทางอย่างเดียว

---

## Big Picture

```text
                    ecosystem-brief
                  "Shared Mental Model"
                           │
              ┌────────────┴────────────┐
              │                         │
           HUMAN                       AI
              │                         │
              └────────────┬────────────┘
                           ▼
                    ecosystem map
                           │
           ┌───────────────┼───────────────┐
           ▼               ▼               ▼
     capabilities       contracts        owners
           └───────────────┼───────────────┘
                           ▼
                    agent-platform
                           │
               ┌───────────┼───────────┐
               ▼           ▼           ▼
            Harness       MCP        Skills
               └───────────┼───────────┘
                           ▼
                     Applications
                           │
                           ▼
                ecosystem-intelligence
                           │
                      detect drift
                           │
                           ▼
                    ecosystem-brief
```

---

## Layers

> 🟡 **Proposed / Under Review** — layer model นี้เป็นข้อเสนอตั้งต้น ยังไม่ผ่านการยืนยันจากเจ้าของ repo
> ดูสถานะการ review ที่ [`docs/ecosystem.md#สถานะการ-review`](docs/ecosystem.md#สถานะการ-review)

| Layer | ทำอะไร | Repo หลัก |
|---|---|---|
| **L0 Foundation** | มาตรฐาน / convention / governance | `code-standards`, `workshop-github` |
| **L1 Model & Provider** | คัดและตรวจสอบ LLM ที่ใช้ได้จริง | `free-llm-registry`, `*-free-model` |
| **L2 Gateway** | ทางออก LLM ของ ecosystem | `llm-gateway` |
| **L3 Platform** | รากฐานการสร้าง/ควบคุม agent + knowledge | `agent-platform`, `enterprise-knowledge` |
| **L4 Harness & Agent** | บังคับ workflow ให้ agent ทำงานถูกขั้น | `opencode-as-hermes`, `ai-web-harness` |
| **L5 Tools / MCP / Skills** | ความสามารถที่ agent เรียกใช้ | `cf-odoo-mcp-server`, `odoo-mcp-chatgpt`, `personal-ai-plugin` |
| **L6 Application** | ของที่ผู้ใช้จริงสัมผัส | `botforge`, `hermes-line-bot`, `care-agent-platform` |
| **L7 Factory & Delivery** | ส่งมอบ / orchestration / DevOps | `devfactory-core` |
| **L8 Intelligence** | มองย้อนกลับมาที่ ecosystem ตัวเอง | `ecosystem-intelligence` |

---

## กติกาของ repo นี้

1. **บาง** — ถ้าเริ่มหนา แปลว่ากำลังกลายเป็น platform อีกตัว
2. **ไม่ duplicate implementation** — รายละเอียดอยู่ใน repo เจ้าของ ที่นี่แค่ชี้ทาง
3. **ไม่แย่งงาน `ecosystem-intelligence`** — ที่นี่บอก "ควรเป็นอะไร" ไม่ใช่ "ตอนนี้เป็นอะไร"
4. **ลิงก์ > คัดลอก** — เจอข้อมูลซ้ำเมื่อไหร่ ให้ลบแล้วลิงก์ไปแทน
5. **ไม่ฟันธงแทนเจ้าของ repo** — ข้อเสนอที่ยังไม่ผ่าน review ต้องติดป้าย 🟡 Proposed เสมอ

---

## สถานะ

🚧 **Phase 1 — Ecosystem Map**

- [x] วางโครงและ layer model (🟡 proposed)
- [x] วาง schema ของ repository registry + capability index
- [ ] เติม `owner` / `depends_on` / `consumed_by` ให้ครบ — **งานถัดไป**
- [ ] ยืนยัน boundary B1–B5 แล้วแยกไป `docs/contracts.md`
- [ ] ให้แต่ละ repo owner review ส่วนของตัวเอง
- [ ] ต่อ `ecosystem-intelligence` ให้ตรวจ drift อัตโนมัติ

ดู roadmap เต็มที่ [`docs/ecosystem.md#roadmap`](docs/ecosystem.md#roadmap)
