# Architecture

> 🟡 **Proposed / Under Review** — ภาพและ boundary ในหน้านี้เป็นข้อเสนอของ `ecosystem-brief`
> ยังไม่ผ่านการยืนยันจากเจ้าของ repo — ดู [สถานะการ review](ecosystem.md#สถานะการ-review)

ภาพ mental model กลาง — ถ้าคนหรือ AI เห็นภาพนี้ตรงกัน ที่เหลือจะคุยกันรู้เรื่อง

## Runtime View

```text
                       ┌─────────────────────┐
                       │   Users / Channels  │
                       │  LINE · Web · CLI   │
                       └──────────┬──────────┘
                                  │
                    ┌─────────────▼─────────────┐
                    │  L6  Applications / Bots  │
                    │  botforge · hermes-line   │
                    │  care-agent-platform      │
                    └─────────────┬─────────────┘
                                  │
                    ┌─────────────▼─────────────┐
                    │  L4  Harness & Agent      │
                    │  opencode-as-hermes       │
                    │  ai-web-harness           │
                    └───────┬───────────┬───────┘
                            │           │
              ┌─────────────▼──┐   ┌────▼──────────────┐
              │ L3 agent-      │   │ L5 Tools / MCP /  │
              │    platform    │◄──┤    Skills         │
              │ + enterprise-  │   │ *-mcp-* · plugins │
              │   knowledge    │   └───────────────────┘
              └───────┬────────┘
                      │  contracts
              ┌───────▼────────┐
              │ L2 llm-gateway │   ← ทางออกสู่ LLM ทางเดียว
              └───────┬────────┘
                      │
        ┌─────────────┼─────────────┬──────────────┐
        ▼             ▼             ▼              ▼
    OpenAI       Qwen / Ollama   Free tier    Thai providers
                                              (Typhoon, SEA-LION)
                      ▲
                      │ curated & verified by
              ┌───────┴──────────┐
              │ L1 free-llm-     │
              │    registry      │
              │    *-free-model  │
              └──────────────────┘
```

## Governance View

ชั้นที่ไม่ได้อยู่ใน request path แต่คุมทั้ง ecosystem

```text
   L0 Foundation                      L7 Factory & Delivery
   code-standards                     devfactory-core
   workshop-github                            │
        │                                     │ deploys / orchestrates
        │ กำหนดกติกาให้                        ▼
        └──────────────► ทุก repo ◄────────────┘
                            │
                            │ observed by
                            ▼
                  L8 ecosystem-intelligence
                            │
                            │ compares against
                            ▼
                     ecosystem-brief   ← repo นี้
                     (desired state)
```

**loop ที่เราอยากได้:**

```text
   brief นิยามว่า ecosystem ควรเป็นอย่างไร
              │
              ▼
   intelligence ตรวจของจริงว่าเป็นอย่างไร
              │
              ▼
   drift ที่เจอ → กลับมาแก้ brief หรือแก้ repo
              │
              └──────────► วนใหม่
```

---

## Boundaries

🟡 **ทั้งหมดยัง Proposed** — ขอบเขตที่เสนอว่าไม่ควรข้าม เพื่อกันไม่ให้ ecosystem กลายเป็นก้อนเดียว
แต่ละข้อต้องให้ repo ที่ระบุใน [สถานะการ review](ecosystem.md#สถานะการ-review) ยืนยันก่อน

| # | Boundary | กฎ | ถ้าละเมิดจะเกิดอะไร |
|---|---|---|---|
| B1 | **Gateway boundary** | ห้าม L3–L6 เรียก LLM provider ตรง ต้องผ่าน `llm-gateway` | เปลี่ยน provider ทีต้องแก้ทุก repo, คุมต้นทุน/quota ไม่ได้ |
| B2 | **Contract boundary** | ความสามารถข้าม repo ต้องมี contract ที่ `agent-platform` เป็นเจ้าของ | repo ผูกกันแบบ implicit แก้ที่นึงพังอีกที่ |
| B3 | **Tool boundary** | MCP/Skill ห้ามมี business logic ของ domain | tool ใช้ซ้ำไม่ได้ กลายเป็น application ปลอมตัว |
| B4 | **Knowledge boundary** | การค้นความรู้ต้องผ่าน contract ของ `enterprise-knowledge` | RAG งอกหลายตัว ผลลัพธ์ไม่ตรงกัน |
| B5 | **Map boundary** | `ecosystem-brief` ห้ามเก็บ implementation detail | brief เก่าเร็ว แล้วไม่มีใครเชื่อมันอีก |

**สถานะ:** B5 ตกลงแล้ว (เป็นกติกาของ repo นี้เอง) ส่วน B1–B4 ยังรอเจ้าของ repo ยืนยัน
เมื่อยืนยันแล้วให้ย้ายรายละเอียดไป `docs/contracts.md` แล้วเหลือแค่สรุปที่นี่

**ระหว่างที่ยังไม่ยืนยัน:** ใช้ boundary เหล่านี้เป็น *คำถามที่ควรถามใน review*
ไม่ใช่กฎที่ใช้ block PR ของทีมอื่น

---

## จุดที่ยังไม่นิ่ง (Open Questions)

- [ ] `agent-platform` กับ `devfactory-core` แบ่ง orchestration กันตรงไหน
- [ ] `enterprise-knowledge` เป็น component ใน L3 หรือควรแยกเป็นชั้นของตัวเอง
- [ ] harness หลายตัว (`opencode-as-hermes`, `ai-web-harness`, botforge engines) — จะรวมเป็น contract เดียวหรือปล่อยให้แตกต่างตาม domain
- [ ] `cloudflare-os` อยู่ชั้นไหน — runtime, application, หรือทั้งสอง
- [ ] repo ตระกูล `poc-*` (มีหลายสิบตัว) จะ archive, merge, หรือคงไว้เป็น experiment layer
