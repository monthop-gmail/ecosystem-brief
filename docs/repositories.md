# Repository Registry

**Core repositories ของ ecosystem** — 22 ตัวที่ต้องรู้จักก่อน
ไม่ใช่รายชื่อทั้งหมด ecosystem มี 219 repositories (public ~140 / private ~79)
ที่เหลือคือ PoC, workshop, งาน domain เฉพาะ และงานลูกค้า

> 📌 repo นี้เป็น public — **private repositories ไม่ถูกระบุชื่อที่นี่** โดยตั้งใจ
> registry ฝั่ง private อยู่ที่อื่น (TBD)

หมายเหตุ: คอลัมน์ **Owner** ยังว่างทั้งหมด — รอทีมยืนยัน อย่าเดา

---

## L0 — Foundation

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`code-standards`](https://github.com/monthop-gmail/code-standards) | มาตรฐานโค้ดก่อนขึ้น production 11 ข้อ พร้อมหลักฐานเชิงทดลอง | Active | _TBD_ |
| [`workshop-github`](https://github.com/monthop-gmail/workshop-github) | Handbook + template ทำให้ทุก repo เป็นมาตรฐานเดียวกัน | Active | _TBD_ |

## L1 — Model & Provider

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`free-llm-registry`](https://github.com/monthop-gmail/free-llm-registry) | รวบรวม → normalize → verify → จัดอันดับ free LLM/provider เปิดเป็น REST API | Active | _TBD_ |
| [`opencode-free-model`](https://github.com/monthop-gmail/opencode-free-model) | ตรวจว่า free model ตัวไหนใช้กับ opencode ได้จริง (เน้นโมเดลไทย) | Active | _TBD_ |
| [`hermes-free-model`](https://github.com/monthop-gmail/hermes-free-model) | ตรวจ context floor / quota สำหรับ Hermes Agent | Active | _TBD_ |
| [`openworker-free-model`](https://github.com/monthop-gmail/openworker-free-model) | ตรวจ free model + ชั้นความเสี่ยงของ tool สำหรับ OpenWorker | Active | _TBD_ |

## L2 — Gateway

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`llm-gateway`](https://github.com/monthop-gmail/llm-gateway) | **ทางออกสู่ LLM ทางเดียวของ ecosystem** — LiteLLM + Open WebUI, OpenAI-compatible | Active | _TBD_ |

## L3 — Platform

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`agent-platform`](https://github.com/monthop-gmail/agent-platform) | รากฐานการสร้าง เชื่อม ควบคุม และ scale agent — **เจ้าของ contract กลาง** | Active | _TBD_ |
| [`enterprise-knowledge`](https://github.com/monthop-gmail/enterprise-knowledge) | Knowledge plane — hybrid RAG หลัง contract `knowledge.search` พร้อม ACL/tenant isolation | Active | _TBD_ |

## L4 — Harness & Agent

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`opencode-as-hermes`](https://github.com/monthop-gmail/opencode-as-hermes) | ทำให้ opencode เป็น personal agent — skills + memory + cron + LINE | Active | _TBD_ |
| [`ai-web-harness`](https://github.com/monthop-gmail/ai-web-harness) | Harness บังคับ workflow เว็บ: requirement → design → implement → test → review → fix | Active | _TBD_ |

## L5 — Tools / MCP / Skills

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`cf-odoo-mcp-server`](https://github.com/monthop-gmail/cf-odoo-mcp-server) | Odoo MCP บน Cloudflare Workers — stateless HTTP, JSON-RPC | Active | _TBD_ |
| [`odoo-mcp-chatgpt`](https://github.com/monthop-gmail/odoo-mcp-chatgpt) | Odoo MCP สำหรับ ChatGPT ผ่าน Secure MCP Tunnel (outbound-only) | Active | _TBD_ |
| [`personal-ai-plugin`](https://github.com/monthop-gmail/personal-ai-plugin) | Personal agent plugin ใช้ได้กับ AI tool 12 ตัว | Active | _TBD_ |
| [`mcp-project-template`](https://github.com/monthop-gmail/mcp-project-template) | Template สร้าง MCP server ตัวใหม่ (`xxx-mcp-claude`) | Dormant | _TBD_ |

> ตระกูล `*-mcp-claude` (odoo, rag, chat, iot, youtuber, transcript, thudong, samathi101 …) เกิดจาก template ตัวนี้
> ยังไม่ตัดสินใจว่าจะรวมเป็น registry เดียวหรือแยกต่อไป — ดู [architecture.md](architecture.md#จุดที่ยังไม่นิ่ง-open-questions)

## L6 — Application

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`botforge`](https://github.com/monthop-gmail/botforge) | สร้าง AI LINE Bot ด้วยคำสั่งเดียว — 9 engines | Active | _TBD_ |
| [`hermes-line-bot`](https://github.com/monthop-gmail/hermes-line-bot) | Hermes Agent ต่อ LINE OA โดยตรง ต้นแบบของ hermes engine ใน botforge | Active | _TBD_ |
| [`care-agent-platform`](https://github.com/monthop-gmail/care-agent-platform) | AI external memory & care companion — domain consumer ของ `agent-platform` | Active | _TBD_ |
| [`botforge-zabbix`](https://github.com/monthop-gmail/botforge-zabbix) | Agent ดูแล Zabbix monitoring ผ่าน LINE OA | Active | _TBD_ |
| [`cloudflare-os`](https://github.com/monthop-gmail/cloudflare-os) | Agent workspace บน Cloudflare Workers — ชั้นยังไม่นิ่ง | Active | _TBD_ |

## L7 — Factory & Delivery

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`devfactory-core`](https://github.com/monthop-gmail/devfactory-core) | Governance-first infrastructure สำหรับ autonomous DevOps + multi-agent orchestration | Active | _TBD_ |

## L8 — Intelligence

| Repo | Role | Status | Owner |
|---|---|---|---|
| [`ecosystem-intelligence`](https://github.com/monthop-gmail/ecosystem-intelligence) | Engineering intelligence ข้ามทีม/ข้าม repo — ตอบว่าควรสร้างอะไรและทำไม | Active | _TBD_ |

---

## ยังไม่ได้จัดชั้น

repo กลุ่มใหญ่ที่ยังไม่ได้ mapping — จัดในรอบถัดไป

| กลุ่ม | ตัวอย่าง | ประเด็น |
|---|---|---|
| Coding agents | `gocode`, `adkcode`, `mini-claude-code`, `opencode` | เป็น engine ของ botforge หรือ product แยก |
| LINE bot experiments | `cc-line-*`, `oc-line-*`, `antigravity-line` | น่าจะ archive ได้แล้วเมื่อ botforge นิ่ง |
| Legal domain | `legal-th-*`, `lawform-*`, `ecosystem-legal-service` | เป็น vertical ที่ควรมี layer map ของตัวเอง |
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

> สถานะในตารางนี้อ้างอิงวันที่แก้ไขล่าสุด ณ 2026-08-30
> **สถานะจริงเป็นหน้าที่ของ [`ecosystem-intelligence`](https://github.com/monthop-gmail/ecosystem-intelligence)** — ที่นี่เก็บแค่เจตนา
