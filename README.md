# ecosystem-brief

> **Start here.** แผนที่กลางของ Monthop AI Ecosystem — สำหรับทั้งคนและ AI

repo นี้ **ไม่ใช่** implementation และ **ไม่ใช่** source of truth
มันคือ **Map of Truth** — บอกว่า ecosystem เรามีอะไร อยู่ชั้นไหน repo ไหนเป็นเจ้าของ และถ้าจะทำของใหม่ควรไปแก้ตรงไหน

**เป้าหมาย: เปิดอ่าน 1 นาทีแล้วเห็นภาพเดียวกัน**

---

## Big Picture

```text
                    ecosystem-brief
                      "Start here"
                           │
           ┌───────────────┼───────────────┐
           ▼               ▼               ▼
        Humans          AI Agents        Teams
           └───────────────┼───────────────┘
                           ▼
                  Shared Mental Model
                           │
           ┌───────────────┼───────────────┐
           ▼               ▼               ▼
     agent-platform    llm-gateway      harness
           └───────────────┼───────────────┘
                           ▼
                   Actual Ecosystem
                           │
                           ▼
                ecosystem-intelligence
```

- `ecosystem-brief` = **desired state** (คนนิยาม)
- `ecosystem-intelligence` = **observed state** (เครื่องสังเกต แล้วบอกว่า drift ตรงไหน)

---

## Layers

| Layer | ทำอะไร | Repo หลัก |
|---|---|---|
| **L0 Foundation** | มาตรฐาน / convention / governance | `code-standards`, `workshop-github` |
| **L1 Model & Provider** | คัดและตรวจสอบ LLM ที่ใช้ได้จริง | `free-llm-registry`, `*-free-model` |
| **L2 Gateway** | ทางออก LLM ทางเดียวของทั้ง ecosystem | `llm-gateway` |
| **L3 Platform** | รากฐานการสร้าง/ควบคุม agent + knowledge | `agent-platform`, `enterprise-knowledge` |
| **L4 Harness & Agent** | บังคับ workflow ให้ agent ทำงานถูกขั้น | `opencode-as-hermes`, `ai-web-harness` |
| **L5 Tools / MCP / Skills** | ความสามารถที่ agent เรียกใช้ | `cf-odoo-mcp-server`, `odoo-mcp-chatgpt`, `personal-ai-plugin` |
| **L6 Application** | ของที่ผู้ใช้จริงสัมผัส | `botforge`, `hermes-line-bot`, `care-agent-platform` |
| **L7 Factory & Delivery** | ส่งมอบ / orchestration / DevOps | `devfactory-core` |
| **L8 Intelligence** | มองย้อนกลับมาที่ ecosystem ตัวเอง | `ecosystem-intelligence` |

---

## Where to start

| คุณคือ | อ่านอันนี้ |
|---|---|
| คนเพิ่งเข้าทีม | [`docs/ecosystem.md`](docs/ecosystem.md) |
| อยากเห็นภาพ architecture | [`docs/architecture.md`](docs/architecture.md) |
| หาว่า repo ไหนทำอะไร | [`docs/repositories.md`](docs/repositories.md) |
| **AI coding agent** | **[`ai/context.md`](ai/context.md) — อ่านก่อนแตะ repo ใด ๆ** |

---

## กติกาของ repo นี้

1. **บาง** — ถ้าเริ่มหนา แปลว่ากำลังกลายเป็น platform อีกตัว
2. **ไม่ duplicate implementation** — รายละเอียดอยู่ใน repo เจ้าของ ที่นี่แค่ชี้ทาง
3. **ไม่แย่งงาน `ecosystem-intelligence`** — ที่นี่บอก "ควรเป็นอะไร" ไม่ใช่ "ตอนนี้เป็นอะไร"
4. **ลิงก์ > คัดลอก** — เจอข้อมูลซ้ำเมื่อไหร่ ให้ลบแล้วลิงก์ไปแทน

---

## สถานะ

🚧 **Phase 1 — Ecosystem Map** (กำลังทำ)

- [x] วางโครงและ layer model
- [ ] เติม repository registry ให้ครบและยืนยัน owner
- [ ] เติม contract / boundary ระหว่าง layer
- [ ] ให้แต่ละทีม review ส่วนของตัวเอง
- [ ] ต่อ `ecosystem-intelligence` ให้ตรวจ drift อัตโนมัติ

ดู roadmap เต็มที่ [`docs/ecosystem.md#roadmap`](docs/ecosystem.md#roadmap)
