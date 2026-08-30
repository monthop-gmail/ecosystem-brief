# Ecosystem Overview

> One ecosystem, one shared mental model.

## ปัญหาที่ repo นี้แก้

ตอนนี้ ecosystem มี **219 repositories** (public ~140 / private ~79) และยังโตต่อ
ของเยอะขนาดนี้ทำให้เกิดอาการ:

- คนใหม่เข้ามาไม่รู้จะเริ่มอ่านตรงไหน
- AI agent แต่ละตัวตีความ architecture คนละแบบ
- ความสามารถเดิมถูกสร้างซ้ำ เพราะไม่รู้ว่ามีอยู่แล้ว
- ไม่รู้ว่า repo ไหนคือ source of truth ของเรื่องไหน

`ecosystem-brief` แก้ข้อเดียว: **ทำให้ทุกคนและทุก agent เริ่มจากแผนที่เดียวกัน**

---

## ecosystem-brief ไม่ใช่อะไร

| ไม่ใช่ | เพราะ |
|---|---|
| ไม่ใช่ platform | ไม่มี code ที่รันได้ ไม่มี service |
| ไม่ใช่ source of truth ของ implementation | source of truth อยู่ใน repo เจ้าของเสมอ |
| ไม่ใช่ wiki ที่เขียนทุกอย่าง | เขียนเฉพาะสิ่งที่ช่วยให้ "หาเจอ" และ "ไม่ทำซ้ำ" |
| ไม่ใช่รายงานสถานะ | สถานะจริงเป็นหน้าที่ของ `ecosystem-intelligence` |

```text
ecosystem-brief
      │
      │ maps  ── "มีอะไร / ไปทางไหน"
      ▼
┌────────────────────────────┐
│ agent-platform             │  ← source of truth ตัวจริง
│ llm-gateway                │
│ botforge                   │
│ ai-web-harness             │
│ devfactory-core            │
│ ecosystem-intelligence     │
│ ...                        │
└────────────────────────────┘
```

---

## Layer Model

เราแบ่ง ecosystem เป็น 9 ชั้น เรียงจากรากขึ้นไปหาผู้ใช้

### L0 — Foundation
มาตรฐาน convention และ governance ที่ทุก repo ต้องเคารพ
ไม่มี runtime แต่กำหนดว่า "โค้ดแบบไหนถึงขึ้น production ได้"

### L1 — Model & Provider
คัด ทดสอบ และจัดอันดับ LLM ที่ใช้ได้จริง โดยเฉพาะ free tier และ provider ไทย
ผลลัพธ์ของชั้นนี้ป้อนให้ L2 เป็นคนตัดสินใจ route

### L2 — Gateway
**ทางออกสู่ LLM ทางเดียวของทั้ง ecosystem** ทุกอย่างที่อยู่เหนือชั้นนี้ต้องคุยผ่าน OpenAI-compatible API เท่านั้น
ห้าม application เรียก provider ตรง

### L3 — Platform
รากฐานการสร้าง เชื่อม ควบคุม และ scale agent รวมถึง knowledge plane (RAG)
เป็นที่อยู่ของ **contract กลาง** ที่ชั้นบนต้องทำตาม

### L4 — Harness & Agent
ตัว agent และกรอบที่บังคับให้ agent ทำงานเป็นขั้นตอน (requirement → design → implement → test → review)
harness คือสิ่งที่ทำให้ผลลัพธ์ของ AI คาดเดาได้

### L5 — Tools / MCP / Skills
ความสามารถที่ agent หยิบไปใช้ — MCP server, skill, plugin
ชั้นนี้ต้องบางและ composable ไม่ควรมี business logic

### L6 — Application
ของที่ผู้ใช้จริงสัมผัส — LINE bot, care companion, งาน domain เฉพาะ
ประกอบจากชั้นล่างทั้งหมด ไม่ควรสร้างความสามารถใหม่เอง

### L7 — Factory & Delivery
ส่งมอบ orchestration และ DevOps แบบ governance-first

### L8 — Intelligence
มองย้อนกลับมาที่ ecosystem ตัวเอง — repo ไหน drift, contract ไหนถูกละเมิด, ควรสร้างอะไรต่อ

---

## ความสัมพันธ์หลัก

```text
   L8 ecosystem-intelligence ──── observes ────┐
                                               │
   L7 devfactory-core ──── delivers ───────────┤
                                               │
   L6 Applications  (botforge, hermes-line-bot, care-agent-platform)
            │ uses
            ▼
   L5 Tools / MCP / Skills
            │ registered in
            ▼
   L4 Harness & Agent
            │ built on
            ▼
   L3 agent-platform + enterprise-knowledge
            │ calls
            ▼
   L2 llm-gateway          ← ทางออกเดียว
            │ routes to
            ▼
   L1 Model & Provider
            ▲
            │ governed by
   L0 Foundation (standards / conventions)
```

**กฎข้ามชั้นที่สำคัญ**

1. ข้ามชั้นลงได้ **ไม่เกิน 1 ชั้น** — ถ้าต้องข้ามมากกว่านั้น แปลว่า contract หายไปหนึ่งตัว
2. ห้ามพึ่งพาย้อนขึ้น — L3 ต้องไม่รู้จัก L6
3. L2 คือคอขวดโดยตั้งใจ — ทุก LLM call ผ่านที่นี่ที่เดียว

> ⚠️ ข้อ 1–3 เป็นข้อเสนอเริ่มต้น ยังต้องให้ทีมยืนยัน — ดู [ai/context.md](../ai/context.md)

---

## Roadmap

| Phase | ทำอะไร | สถานะ |
|---|---|---|
| **1** | Ecosystem Map — README + layer + repository registry | 🚧 กำลังทำ |
| **2** | Architecture Map — boundary และภาพ mental model กลาง | ⏳ |
| **3** | AI Context — `ai/context.md` + decision flow ให้ agent | 🚧 ร่างแล้ว รอ review |
| **4** | เชื่อม `ecosystem-intelligence` ให้ตรวจ drift จากของจริง | ⏳ |
| **5** | ให้ `agent-platform` / MCP / Skills ใช้ brief เป็น entry point | ⏳ |

**หลักการเรียงลำดับ:** ทำแผนที่ก่อนแจกเครื่องมือ
ถ้าเริ่มจาก MCP ก่อน เราจะได้ "เครื่องมือที่ยังไม่มีแผนที่"
