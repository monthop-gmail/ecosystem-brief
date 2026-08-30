# Repository Registry

**Core repositories ของ ecosystem** — 22 ตัวที่ต้องรู้จักก่อน
ecosystem ทั้งหมดมี 219 repositories (public ~140 / private ~79) ที่เหลือคือ PoC, workshop,
งาน domain เฉพาะ และงานลูกค้า

> 📌 repo นี้เป็น public — **private repositories ไม่ถูกระบุชื่อที่นี่** โดยตั้งใจ
> registry ฝั่ง private อยู่ที่อื่น (TBD)

---

## Schema

ทุก entry ใน registry ต้องมีครบ 10 field นี้

| Field | หมายถึง | บังคับ |
|---|---|---|
| `repo` | ชื่อ repository | ✅ |
| `purpose` | ทำอะไร — หนึ่งประโยค | ✅ |
| `layer` | L0–L8 | ✅ |
| `owner` | คน/ทีมที่ตัดสินใจแทน repo นี้ได้ | ✅ |
| `status` | Active / Dormant / Deprecated / Archived | ✅ |
| `source_of_truth_for` | **ความสามารถที่ repo นี้เป็นเจ้าของ** — ที่อื่นห้ามสร้างซ้ำ | ✅ |
| `depends_on` | repo ที่ต้องมีก่อน | — |
| `consumed_by` | ใครเรียกใช้ | — |
| `contracts` | contract ที่ repo นี้ประกาศหรือต้องทำตาม | — |
| `canonical_docs` | เอกสารที่ถือเป็นความจริง (ไม่ใช่ไฟล์นี้) | — |

**`source_of_truth_for` คือ field ที่สำคัญที่สุด** — เป็นตัวเดียวที่กัน AI สร้างความสามารถซ้ำ
ถ้ายังเว้นว่าง ถือว่า entry นั้นยังใช้งานไม่ได้จริง

### สัญลักษณ์

| | หมายถึง |
|---|---|
| (ข้อความปกติ) | ยืนยันจาก README/description ของ repo นั้นเอง |
| 🟡 | ข้อเสนอจาก `ecosystem-brief` — **ยังไม่ผ่าน review ของ owner** |
| _TBD_ | ยังไม่มีข้อมูล ต้องไปถาม |

---

## Capability Index

**ตารางที่ AI ควรอ่านก่อนเขียนโค้ดใหม่** — ถามว่า "ความสามารถนี้มีเจ้าของแล้วหรือยัง"

| ความสามารถ | เจ้าของ | ห้ามสร้างซ้ำที่ไหน |
|---|---|---|
| เรียก LLM / routing / quota / provider key | `llm-gateway` | ทุก repo — ต้องผ่าน gateway เท่านั้น |
| นิยาม contract ระหว่าง agent กับ tool | `agent-platform` 🟡 | ห้ามนิยาม contract เองใน application |
| ค้นความรู้ / RAG / retrieval | `enterprise-knowledge` | ห้ามตั้ง RAG stack ใหม่ |
| ตัดสินว่า model ตัวไหนใช้ได้ | `free-llm-registry` | ห้าม hardcode model list |
| ทดสอบ model กับ agent runtime หนึ่ง ๆ | `*-free-model` | — |
| บังคับ workflow ของ agent | `ai-web-harness` (เว็บ), `opencode-as-hermes` (personal) 🟡 | — |
| สร้าง MCP server ตัวใหม่ | `mcp-project-template` | ห้ามเริ่มจากศูนย์ |
| เข้าถึง Odoo จาก AI | `cf-odoo-mcp-server`, `odoo-mcp-chatgpt` | ห้ามเขียน Odoo client ใหม่ |
| สร้าง LINE bot | `botforge` | ห้ามเขียน LINE webhook ใหม่ |
| มาตรฐานโค้ดก่อนขึ้น production | `code-standards` | — |
| scaffold repo ให้เป็นมาตรฐาน | `workshop-github` | — |
| deploy / orchestrate / DevOps | `devfactory-core` 🟡 | — |
| วัดสถานะจริงของ ecosystem | `ecosystem-intelligence` | **รวมถึง `ecosystem-brief` เองด้วย** |
| นิยามว่า ecosystem ควรเป็นอย่างไร | `ecosystem-brief` | — |

> ⚠️ ตารางนี้ยังไม่ครบ ความสามารถที่ยังหาเจ้าของไม่เจอ ให้เปิด issue อย่าเดา

---

## Registry

### L0 — Foundation

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`code-standards`](https://github.com/monthop-gmail/code-standards) | มาตรฐานโค้ดก่อนขึ้น production 11 ข้อ พร้อมหลักฐานเชิงทดลอง | เกณฑ์คุณภาพโค้ดก่อน production | Active | _TBD_ |
| [`workshop-github`](https://github.com/monthop-gmail/workshop-github) | Handbook + template ทำให้ทุก repo เป็นมาตรฐานเดียวกัน | โครงสร้าง repo มาตรฐาน, GitHub convention | Active | _TBD_ |

### L1 — Model & Provider

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`free-llm-registry`](https://github.com/monthop-gmail/free-llm-registry) | รวบรวม → normalize → verify → จัดอันดับ free LLM/provider เปิดเป็น REST API | รายชื่อและอันดับ model ที่ใช้ได้จริง | Active | _TBD_ |
| [`opencode-free-model`](https://github.com/monthop-gmail/opencode-free-model) | ตรวจว่า free model ตัวไหนใช้กับ opencode ได้จริง (เน้นโมเดลไทย) | ผลทดสอบ model × opencode | Active | _TBD_ |
| [`hermes-free-model`](https://github.com/monthop-gmail/hermes-free-model) | ตรวจ context floor / quota สำหรับ Hermes Agent | ผลทดสอบ model × Hermes | Active | _TBD_ |
| [`openworker-free-model`](https://github.com/monthop-gmail/openworker-free-model) | ตรวจ free model + ชั้นความเสี่ยงของ tool สำหรับ OpenWorker | ผลทดสอบ model × OpenWorker | Active | _TBD_ |

### L2 — Gateway

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`llm-gateway`](https://github.com/monthop-gmail/llm-gateway) | OpenAI-compatible gateway (LiteLLM + Open WebUI) ออก API token เองได้ | **LLM routing, provider key, quota, token ทั้ง ecosystem** | Active | _TBD_ |

### L3 — Platform

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`agent-platform`](https://github.com/monthop-gmail/agent-platform) | รากฐานการสร้าง เชื่อม ควบคุม และ scale agent ข้าม enterprise application | 🟡 contract กลางระหว่าง layer, agent runtime model | Active | _TBD_ |
| [`enterprise-knowledge`](https://github.com/monthop-gmail/enterprise-knowledge) | Knowledge plane ของ `agent-platform` — hybrid RAG (pgvector + RRF + cross-encoder) | contract `knowledge.search`, ACL/tenant isolation, evaluation | Active | _TBD_ |

### L4 — Harness & Agent

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`opencode-as-hermes`](https://github.com/monthop-gmail/opencode-as-hermes) | ทำให้ opencode เป็น personal agent — skills + memory + cron + LINE | 🟡 personal agent workflow | Active | _TBD_ |
| [`ai-web-harness`](https://github.com/monthop-gmail/ai-web-harness) | Harness บังคับ workflow: requirement → design → implement → test → review → fix | workflow การสร้างเว็บด้วย AI | Active | _TBD_ |

### L5 — Tools / MCP / Skills

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`cf-odoo-mcp-server`](https://github.com/monthop-gmail/cf-odoo-mcp-server) | Odoo MCP บน Cloudflare Workers — stateless HTTP, JSON-RPC | การเข้าถึง Odoo แบบ serverless | Active | _TBD_ |
| [`odoo-mcp-chatgpt`](https://github.com/monthop-gmail/odoo-mcp-chatgpt) | Odoo MCP สำหรับ ChatGPT ผ่าน Secure MCP Tunnel (outbound-only) | การเข้าถึง Odoo จาก ChatGPT | Active | _TBD_ |
| [`personal-ai-plugin`](https://github.com/monthop-gmail/personal-ai-plugin) | Personal agent plugin ใช้ได้กับ AI tool 12 ตัว | note/TODO/research/memory ของ personal agent | Active | _TBD_ |
| [`mcp-project-template`](https://github.com/monthop-gmail/mcp-project-template) | Template สร้าง MCP server ตัวใหม่ (`xxx-mcp-claude`) | โครงสร้างมาตรฐานของ MCP server | Dormant | _TBD_ |

### L6 — Application

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`botforge`](https://github.com/monthop-gmail/botforge) | สร้าง AI LINE Bot ด้วยคำสั่งเดียว — 9 engines | การต่อ LINE OA เข้ากับ coding agent | Active | _TBD_ |
| [`hermes-line-bot`](https://github.com/monthop-gmail/hermes-line-bot) | Hermes Agent ต่อ LINE OA โดยตรง — ต้นแบบของ hermes engine ใน botforge | pattern การให้ agent เป็นเจ้าของ LINE channel เอง | Active | _TBD_ |
| [`care-agent-platform`](https://github.com/monthop-gmail/care-agent-platform) | AI external memory & care companion สำหรับผู้สูงอายุ | domain: care / external memory | Active | _TBD_ |
| [`botforge-zabbix`](https://github.com/monthop-gmail/botforge-zabbix) | Agent ดูแล Zabbix monitoring ผ่าน LINE OA | domain: infrastructure monitoring | Active | _TBD_ |
| [`cloudflare-os`](https://github.com/monthop-gmail/cloudflare-os) | Agent workspace บน Cloudflare Workers | 🟡 _ชั้นยังไม่นิ่ง — ดู open questions_ | Active | _TBD_ |

### L7 — Factory & Delivery

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`devfactory-core`](https://github.com/monthop-gmail/devfactory-core) | Governance-first infrastructure สำหรับ autonomous DevOps + multi-agent orchestration | 🟡 การ deploy และ orchestrate agent fleet | Active | _TBD_ |

### L8 — Intelligence

| Repo | Purpose | Source of truth for | Status | Owner |
|---|---|---|---|---|
| [`ecosystem-intelligence`](https://github.com/monthop-gmail/ecosystem-intelligence) | Engineering intelligence ข้ามทีม/ข้าม repo — ตอบว่าควรสร้างอะไรและทำไม | **สถานะจริงของ ecosystem, drift detection** | Active | _TBD_ |

---

## Relationships

`depends_on` / `consumed_by` / `contracts` / `canonical_docs`
ส่วนใหญ่ยังว่าง — **ต้องยืนยันจาก repo จริง ห้ามเดา**

| Repo | Depends on | Consumed by | Contracts | Canonical docs |
|---|---|---|---|---|
| `llm-gateway` | HuggingFace / vLLM / Ollama / cloud providers | 🟡 ทุก repo ที่เรียก LLM | OpenAI-compatible API | repo README |
| `agent-platform` | 🟡 `llm-gateway` | `care-agent-platform` | _TBD_ | repo README |
| `enterprise-knowledge` | `agent-platform` | 🟡 agent ที่ต้องใช้ RAG | `knowledge.search` | repo README |
| `care-agent-platform` | `agent-platform`, pstack | — | _TBD_ | repo README |
| `hermes-line-bot` | `llm-gateway` (LiteLLM) | `botforge` (hermes engine) | _TBD_ | repo README |
| `botforge-zabbix` | `botforge`, opencode, zabbix-mcp-server | — | _TBD_ | repo README |
| `mcp-project-template` | — | ตระกูล `*-mcp-claude` | _TBD_ | repo README |
| `botforge` | 🟡 `llm-gateway` | `botforge-zabbix` | _TBD_ | repo README |
| _(อื่น ๆ)_ | _TBD_ | _TBD_ | _TBD_ | repo README |

> ตระกูล `*-mcp-claude` (odoo, rag, chat, iot, youtuber, transcript, thudong, samathi101 …) เกิดจาก `mcp-project-template`
> ยังไม่ตัดสินใจว่าจะรวมเป็น registry เดียวหรือแยกต่อไป — ดู [architecture.md](architecture.md#จุดที่ยังไม่นิ่ง-open-questions)

---

## ยังไม่ได้จัดชั้น

| กลุ่ม | ตัวอย่าง | ประเด็น |
|---|---|---|
| Coding agents | `gocode`, `adkcode`, `mini-claude-code`, `opencode` | เป็น engine ของ botforge หรือ product แยก |
| LINE bot experiments | `cc-line-*`, `oc-line-*`, `antigravity-line` (~14 ตัว) | น่าจะ archive ได้แล้วเมื่อ botforge นิ่ง |
| Legal domain | `legal-th-*`, `lawform-*`, `ecosystem-legal-service` | vertical ที่ควรมี layer map ของตัวเอง |
| Odoo domain | `thaiacc-odoo`, `l10n-thailand`, `odoo-19-migration-guide` | ต่อกับ ecosystem ตรงไหน |
| Meditation / vidhisa | `samathi101-*`, `vidhisa-49m*`, `tripitaka-*` | product line แยก |
| PoC | `poc-*` (หลายสิบ) | archive / merge / คงไว้เป็น experiment layer |

---

## เกณฑ์การจัดสถานะ

| Status | หมายถึง |
|---|---|
| **Active** | มีการเปลี่ยนแปลงภายใน 60 วัน และยังเป็นทางเดินหลัก |
| **Dormant** | ยังใช้ได้แต่ไม่มีคนแตะ |
| **Deprecated** | มีตัวแทนแล้ว อย่าเริ่มงานใหม่ที่นี่ |
| **Archived** | อ่านอย่างเดียว |

> สถานะในตารางนี้อ้างอิงวันที่แก้ไขล่าสุด ณ 2026-08-30 และเป็น **เจตนา** ไม่ใช่การวัด
> **สถานะจริงเป็นหน้าที่ของ [`ecosystem-intelligence`](https://github.com/monthop-gmail/ecosystem-intelligence)**
