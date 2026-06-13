# Speaker Script TH - Chapters 1-8

รูปแบบ: `Key message` คือประเด็นที่ผู้เรียนต้องจำจาก slide นั้น และ `Speaker script` คือสคริปต์พูดภาษาไทย โดยคง technical words สำคัญเป็น English

## Chapter 1

### 1.1 Traditional SDLC vs. Agentic SDLC Pipeline Comparison

**Key message:** Agentic SDLC เปลี่ยน delivery จาก sequential handoff เป็น parallel, AI-augmented workflow ที่ feedback loop สั้นลงมาก

**Speaker script:** Slide นี้ให้ดู contrast ระหว่าง Traditional SDLC กับ Agentic SDLC ก่อนครับ ฝั่งซ้ายคือ workflow แบบเดิมที่ PM, Developer, Tester, DevOps ส่งงานต่อกันเป็นทอด ๆ ทำให้ feedback มาช้าและเจอ bug ตอนท้าย ฝั่งขวา Claude Code เข้ามาช่วยทุก role พร้อมกัน ตั้งแต่ AI-drafted PRD, pair programming, auto code review, generated tests ไปจนถึง CI/CD และ incident response ประเด็นสำคัญไม่ใช่ AI มาแทนคน แต่คือ AI ทำให้ team ทำงานแบบ parallel และลด handoff lag ได้

### 1.2 Agentic Team Roles - Claude Code Orchestration

**Key message:** Claude Code เป็น orchestrator ที่ช่วย PM, Developer, Tester และ DevOps สร้าง artifact ของตัวเองพร้อมกัน

**Speaker script:** ตรงนี้เรามอง team เป็น 4 quadrant ครับ PM ใช้ AI ช่วยทำ PRD, sprint board และ user stories Developer ใช้ AI ช่วย architecture, code และ review Tester ใช้ AI ช่วย test cases, coverage และ test pyramid ส่วน DevOps ใช้ AI ช่วย Docker, CI/CD และ monitoring ดังนั้น Claude Code ไม่ได้เป็นแค่ code assistant แต่เป็น orchestration layer ที่ช่วยให้ทุก role สร้าง artifact ที่พร้อมส่งต่อกัน

### 1.3 Chat & SMS Architecture - Unified Inbox Pipeline

**Key message:** ตัวอย่างระบบหลักของคอร์สคือ 5-layer architecture: UI, API Gateway, Channel Adapters, RabbitMQ Router และ Data Stores

**Speaker script:** Slide นี้คือ reference architecture ที่เราจะใช้ตลอดคอร์สครับ Message เริ่มจาก Unified Inbox บน Next.js เข้า Go API Gateway แล้วแยกไปที่ Channel Adapters เช่น LINE, Facebook, Slack, WhatsApp, Teams และ SMS จากนั้น RabbitMQ ทำหน้าที่เป็น Message Router ก่อนส่งต่อไป MongoDB สำหรับ message storage, Redis สำหรับ session cache และ ClickHouse สำหรับ analytics ให้จำ flow นี้ไว้ เพราะหลายบทต่อไปจะ zoom เข้าไปทีละ layer

### 1.4 Four Principles of Agentic Development

**Key message:** Agentic Development ต้องมี Human-in-the-Loop, Context Management, Iterative Collaboration และ Auditability

**Speaker script:** หลักการ 4 ข้อนี้คือ guardrail ของการทำงานกับ AI ครับ ข้อแรก Human-in-the-Loop คือ AI propose แต่ human decide ข้อสอง Context Management คือให้ AI เห็นข้อมูลที่เกี่ยวข้องผ่าน CLAUDE.md, PRD และ code spec ข้อสาม Iterative Collaboration คือ generate, review, refine ซ้ำเป็น cycle สั้น ๆ และข้อสี่ Auditability คือทุก artifact ต้อง trace ได้ผ่าน git commits, specs และ decision trail ถ้าขาดข้อใดข้อหนึ่ง ความเร็วจาก AI จะกลายเป็น risk ได้ง่าย

### 1.5 WhatsApp Adapter Feature Timeline

**Key message:** Agentic SDLC สามารถพา feature จาก brief ไปถึง review ได้ในวันเดียว ด้วย parallel role collaboration

**Speaker script:** ตัวอย่างนี้คือวันทำงานหนึ่งวันสำหรับ WhatsApp Adapter ครับ เริ่มจาก PM brief เป็น PRD ต่อด้วย PM และ Developer ทำ architecture plan จากนั้น Developer scaffold adapter, Tester generate tests, Security Subagent ตรวจ vulnerability, DevOps สร้าง Docker และ CI, แล้ว Tester รัน E2E Hook Tests ก่อน PM ทำ sprint review จุดที่อยากให้เห็นคือหลายงานไม่ได้รอต่อคิวกันทั้งหมด แต่ทำแบบ parallel ภายใต้ Claude Code orchestrator

## Chapter 2

### 2.1 Claude Code Permission Modes Spectrum

**Key message:** Permission mode ต้องเลือกตาม risk: Ask Mode สำหรับ safety, Auto-Accept สำหรับ daily work, Full Auto สำหรับ environment ที่ควบคุมได้

**Speaker script:** Permission mode คือสมดุลระหว่าง human oversight กับ AI autonomy ครับ Ask Mode เหมาะกับ new members, production configs และ sensitive operations เพราะต้องขออนุญาตก่อน Auto-Accept เหมาะกับ feature work และ testing ที่ risk ควบคุมได้ ส่วน Full Auto เหมาะกับ CI/CD pipeline, ephemeral environment หรือ disposable container อย่าคิดว่า mode ที่เร็วที่สุดดีที่สุดเสมอ ให้เลือกตาม security policy และ sensitivity ของ environment

### 2.2 CLAUDE.md as the AI Constitution

**Key message:** CLAUDE.md คือ single source of truth ที่ทำให้ทุก AI session ใช้ convention เดียวกัน

**Speaker script:** ให้คิดว่า CLAUDE.md คือ constitution ของ project ครับ ไม่ว่า session จะเป็น PM, Developer, Tester หรือ DevOps ทุกคนอ่าน shared context เดียวกัน PM เห็น scope และ glossary, Developer เห็น architecture และ coding standards, Tester เห็น test conventions, DevOps เห็น infrastructure และ deployment rules ผลลัพธ์คือ output สม่ำเสมอ predict ได้ และลดการอธิบายซ้ำใน prompt แต่ละครั้ง

### 2.3 Role File Inheritance Model

**Key message:** Role files ควร specialize จาก CLAUDE.md ไม่ใช่ duplicate rules ซ้ำกันหลายที่

**Speaker script:** Slide นี้ใช้ mental model แบบ base class กับ specialization ครับ CLAUDE.md เป็น base class เก็บ project overview, architecture, coding standards, API conventions และ git conventions จากนั้น pm.md, dev.md, tester.md, devops.md เพิ่ม instruction เฉพาะ role ของตัวเอง เช่น PRD format, TDD workflow, coverage targets หรือ CI/CD stages หลักคือ specialize, never duplicate ถ้าข้อมูลกลางเปลี่ยน ให้แก้ที่ base ไม่ใช่ไล่แก้ทุกไฟล์

### 2.4 MCP Server Ecosystem

**Key message:** MCP ขยาย Claude Code ให้เข้าถึง tool ภายนอกได้อย่างมีขอบเขตและ config ได้จาก settings.json

**Speaker script:** MCP หรือ Model Context Protocol ทำให้ Claude Code ต่อกับ external systems ได้ เช่น GitHub MCP สำหรับ issues, PRs และ code review, Filesystem MCP สำหรับ scoped file access และ MongoDB MCP สำหรับ query schema หรือ validate data structure ทั้งหมดถูก register ใน settings.json พร้อม environment variables ที่จำเป็น จุดสำคัญคือเราไม่ได้ให้ AI access แบบไร้ขอบเขต แต่ต่อผ่าน protocol และ config ที่ควบคุมได้

### 2.5 Workspace Setup Checklist and File Tree

**Key message:** Workspace ที่ดีต้องมี CLAUDE.md, role files, settings.json, glossary และต้อง commit เข้า git

**Speaker script:** นี่คือ checklist เริ่มต้นก่อนใช้งานจริงครับ ติดตั้ง Claude Code, สร้าง CLAUDE.md, สร้าง role files ใน .claude, configure settings.json สำหรับ hooks, MCP servers และ permissions, เขียน glossary.md แล้ว validate ด้วยแต่ละ role สุดท้ายต้อง commit ทุกอย่างเข้า git เพราะ instructions, settings และ glossary คือ infrastructure ของ AI workflow ไม่ใช่ไฟล์ชั่วคราว

## Chapter 3

### 3.1 Hook Lifecycle

**Key message:** Hooks ทำให้ทุก tool call ถูก validate ก่อนรัน, audit หลังรัน และ gate ก่อนจบงาน

**Speaker script:** Hook lifecycle มี 3 จุดหลักครับ PreToolUse ทำงานก่อน tool execution เพื่อ allow หรือ block, PostToolUse ทำงานหลังได้ result เพื่อ auto-test หรือ audit และ Stop Hook ทำ quality gate ก่อน agent จบงาน ตัวอย่างเช่น command เสี่ยงถูก block ตั้งแต่ PreToolUse, test suite ถูกรันใน PostToolUse และถ้า quality gate fail agent ต้องแก้ก่อนส่งงาน Hooks จึงเป็น automation guardrail ของ AI development

### 3.2 PreToolUse Command Validation Decision Tree

**Key message:** PreToolUse Hook ป้องกัน destructive commands ก่อนที่มันจะถูก execute

**Speaker script:** Flow นี้เริ่มจาก Claude Code propose Bash command แล้ว validate_cmd.py ตรวจ pattern ที่ block เช่น rm -rf, DROP DATABASE, git push --force main, docker system prune หรือ curl pipe bash ถ้าตรง pattern จะถูก reject และ AI ต้องปรับคำสั่งใหม่ ถ้าไม่ตรงจึง allow ให้รันได้ ข้อดีคือเรา enforce safety ที่ system level ไม่ต้องหวังว่า prompt จะเตือน AI ได้ทุกครั้ง

### 3.3 Skills Library

**Key message:** Skills คือ reusable workflow แบบ Markdown ที่ share ผ่าน git และเรียกใช้ซ้ำได้ทั้ง team

**Speaker script:** Skills เปรียบเหมือน slash command ที่ encapsulate workflow สำคัญครับ เช่น /scaffold-adapter สำหรับ Dev, /generate-tests สำหรับ Tester, /sprint-plan สำหรับ PM, /incident-response สำหรับ DevOps หรือ /adr สำหรับ architecture decision เพราะ skills อยู่ใน .claude/skills และ version-controlled ด้วย git ทุกคนใน team ใช้ process เดียวกันได้ ไม่ต้อง copy prompt ยาว ๆ ไปมา

### 3.4 Subagent Architecture

**Key message:** Subagents ช่วยกระจายงานเฉพาะทางแบบ parallel โดยอ่าน codebase เดียวกันแต่ไม่ต้องแย่ง context หลัก

**Speaker script:** Main Claude Code session สามารถ spawn subagents เช่น Security Reviewer, Doc Generator และ Performance Analyzer ให้ทำงานพร้อมกันได้ Security Reviewer ใช้ Opus ตรวจ OWASP, webhook signatures, NoSQL injection และ secrets ส่วนอีก agent ทำ API docs หรือ performance analysis ข้อดีคือแต่ละ subagent focus เฉพาะงานและ report กลับ main session ทำให้ throughput สูงขึ้นโดยไม่ทำให้ context หลักรกเกินไป

### 3.5 Unified settings.json Control Plane

**Key message:** settings.json คือ control plane ที่รวม permissions, hooks และ MCP servers ไว้ในที่เดียว

**Speaker script:** Slide นี้แสดงว่า settings.json ไม่ใช่ config เล็ก ๆ แต่เป็น control plane ของ team ครับ Permissions บอกว่า tool ไหน allowed หรือ denied, Hooks บอกว่า PreToolUse, PostToolUse และ Stop จะเรียก script ไหน, MCP Servers บอกว่า Claude ต่อ GitHub หรือ Filesystem อย่างไร เมื่อทุก tool call ไหลผ่าน pipeline เดียวกัน เราจึงควบคุมทั้ง access, validation และ automation ได้จากไฟล์เดียว

## Chapter 4

### 4.1 RISEN Prompting Framework

**Key message:** RISEN เปลี่ยน raw stakeholder input ให้กลายเป็น structured PRD ด้วย role, instructions, steps, expectations และ narrowing

**Speaker script:** Stakeholder input มักมาแบบกระจัดกระจาย เช่น email, Slack, meeting notes หรือ product feedback RISEN ช่วยจัด prompt ให้ครบ 5 ส่วนคือ Role, Instructions, Steps, End Goal หรือ Expectations และ Narrowing constraints เมื่อ prompt มี structure แบบนี้ Claude Code จะสร้าง PRD ที่มี overview, problem statement, goals, user stories, requirements และ constraints ได้ครบกว่า prompt แบบเล่า ๆ

### 4.2 Three-Phase PRD Generation Workflow

**Key message:** Agentic PRD workflow ลดงานจากหลายวันเหลือไม่กี่ชั่วโมง โดยให้ AI draft และ PM validate

**Speaker script:** Workflow มี 3 phase ครับ Capture คือรวม raw inputs จาก transcript, email, chat และ whiteboard Generation คือให้ Claude Code สร้าง draft PRD ที่ structured และพร้อม review Refinement คือ PM annotate, clarify และ approve เป็น final PRD Traditional process อาจใช้ 3-5 วันเพราะ drafting และ review หลายรอบ แต่ Agentic workflow ให้ AI ทำ first draft แล้ว human ตรวจคุณภาพและตัดสินใจ

### 4.3 User Story Anatomy

**Key message:** User story ที่ดีต้อง observable, measurable และ testable ผ่าน Given/When/Then acceptance criteria

**Speaker script:** ฝั่งซ้ายคือ vague story แบบ "As a user, I want to send messages" พร้อม criteria ว่า "It should be fast" ซึ่งวัดไม่ได้และ test ไม่ได้ ฝั่งขวาใช้ RISEN และ CLAUDE.md context เปลี่ยนเป็น architecture-specific story เช่น support agent ต้องเห็น LINE message ใน unified inbox ภายใน 2 seconds พร้อม Given/When/Then และ audit event ที่ verify ได้ จุดนี้สำคัญมาก เพราะ AI implement ได้ดีเมื่อ requirement testable

### 4.4 Sprint Backlog Dependency Graph

**Key message:** Sprint planning ต้องเห็น story points และ dependencies เพื่อจัดลำดับงานให้ execute ได้จริง

**Speaker script:** Backlog ไม่ใช่ list งานเรียงธรรมดาครับ Slide นี้มี Message Router Core, channel adapters, integration tests และ E2E pipeline พร้อม story points แบบ Fibonacci และ status เช่น Ready, Blocked, In Progress สิ่งที่ต้องดูคือ dependency: adapter บางตัวรอ core router, E2E test รอหลาย component การทำ graph แบบนี้ช่วยให้ AI และ human วาง parallel work ได้ถูก ไม่เริ่มงานที่ยัง blocked

### 4.5 /sprint-plan Skill Cycle

**Key message:** /sprint-plan ทำให้ sprint planning เป็น repeatable process จาก PRD ไปสู่ Markdown และ JSON plan

**Speaker script:** ทุก sprint เราเรียก /sprint-plan เพื่อทำ 6 ขั้นตอนซ้ำได้ครับ อ่าน PRD และ stories, analyze complexity, estimate points, build dependencies, allocate to sprint แล้ว output เป็น MD และ JSON จากนั้น PM review และ refine ก่อน sprint execution พอจบ sprint ก็เอาข้อมูลกลับเข้า retrospective จุดสำคัญคือ planning กลายเป็น workflow ที่ reusable ไม่ใช่งาน manual ที่แต่ละครั้งทำไม่เหมือนกัน

### 4.C Prompt Engineering Frameworks Cheatsheet

**Key message:** Prompt framework ต้องเลือกให้เหมาะกับงาน: งานสั้นใช้ RTF หรือ TAG, งานซับซ้อนใช้ RISEN, SCOPE, RAG หรือ Reflexion

**Speaker script:** Cheatsheet นี้เป็นตัวช่วยเลือก prompt framework ครับ ด้านซ้ายคือ universal prompt formula ที่ควรมี Role, Task, Context, Requirements, Format และ Tone/Style ส่วนตารางด้านขวาช่วยเลือก framework ให้เหมาะกับงาน เช่น RTF สำหรับ prompt ง่าย ๆ, TAG สำหรับ quick instruction, RISEN สำหรับ step-by-step task execution, Few-shot สำหรับ style matching, ReAct สำหรับงานที่ต้อง reasoning และใช้ tools, และ RAG สำหรับตอบจาก documents หรือ sources ประเด็นสำคัญคืออย่าใช้ framework เดียวกับทุกงาน ให้เลือกตาม complexity, context, constraints และ expected output

## Chapter 5

### 5.1 RabbitMQ Fanout Exchange Topology

**Key message:** Fanout exchange ช่วย broadcast message ไปหลาย queues เพื่อแยก storage, analytics และ notification ให้ scale อิสระ

**Speaker script:** เมื่อ message เข้ามาจากหลาย channel ผ่าน adapters แล้ว Message Router ส่งเข้า RabbitMQ Fanout Exchange จากนั้น exchange broadcast ไปยัง Storage Queue, Analytics Queue และ Notification Queue แต่ละ queue มี consumer ของตัวเอง เช่น MongoDB, ClickHouse หรือ WebSocket ข้อดีคือ failure isolation และ independent scaling ถ้า analytics ช้า storage ยังทำงานต่อได้ และถ้า notification มี spike ก็ scale เฉพาะส่วนนั้น

### 5.2 MongoDB Unified Message Schema

**Key message:** UnifiedMessage schema ทำให้ payload จากหลาย channel ถูก normalize แต่ยังเก็บ RawJSON ไว้ครบ

**Speaker script:** LINE, Facebook, Slack, WhatsApp และ Teams มี payload format ต่างกันมาก แต่ระบบต้องมี document model เดียวเพื่อ query และ process ได้ UnifiedMessage จึงมี field กลาง เช่น Channel, ExternalID, SenderID, ReceivedAt, Status, ConversationID, Content, Metadata และ RawJSON สิ่งสำคัญคือ normalize เฉพาะข้อมูลที่ใช้ร่วมกัน แต่เก็บ RawJSON ไว้เพื่อ audit, debug และรองรับ field เฉพาะ channel

### 5.3 Redis Dual-Role Caching Architecture

**Key message:** Redis ทำสองหน้าที่หลักคือ session cache และ rate limiter สำหรับ traffic ที่ real-time

**Speaker script:** Redis ในระบบนี้ไม่ใช่แค่ cache ครับ ฝั่งแรกเป็น Session Cache ใช้ key แบบ session:{channel}:{sender_id} พร้อม sliding TTL 30 นาที เพื่อรู้ว่าข้อความต่อเนื่องอยู่ใน conversation เดิมหรือไม่ ฝั่งที่สองเป็น Rate Limiter ใช้ sorted set และ sliding time window เช่น 22 events ต่อ 60 seconds เพื่อกัน abuse ทั้งสอง role ใช้ความเร็วของ in-memory data store เพื่อป้องกัน database หลักจาก traffic burst

### 5.4 ClickHouse Analytics Pipeline

**Key message:** ClickHouse เหมาะกับ analytics เพราะ batch ingest และ column-oriented storage ทำ aggregate เร็วบน data ปริมาณมาก

**Speaker script:** Analytics pipeline รับ events จาก Analytics Queue เข้า worker แล้ว batch ประมาณ 1000 events หรือ flush ทุก 1-2 seconds ก่อนเขียนลง ClickHouse ด้วย schema แบบ column-oriented เช่น channel, event_time, processing_ms ข้อดีคือ compression สูงและ query aggregate เร็ว เช่น messages per channel per hour, P95 latency และ error rate Slide นี้เน้นว่า operational data กับ analytics data ควรมี pipeline แยกกัน

### 5.5 ADR Structure and Decision Map

**Key message:** ADR บันทึก context, decision, alternatives และ consequences เพื่อให้ architecture decision traceable

**Speaker script:** ADR หรือ Architecture Decision Record ใช้ตอบคำถามว่าเราเลือกอะไรและทำไม ไม่ใช่แค่บอกว่าใช้ technology อะไร โครงสร้างที่ดีควรมี status, context, decision, alternatives considered, consequences และ links ไปยัง related decisions ตัวอย่างเช่นเลือก RabbitMQ, MongoDB, Redis หรือ ClickHouse ต้องเขียนเหตุผลและ trade-offs ไว้ เมื่อทีมกลับมาดูอีก 6 เดือน จะไม่ต้องเดาจาก code ว่าทำไม design เป็นแบบนี้

## Chapter 6

### 6.1 Clean Architecture Three-Layer Pattern

**Key message:** Clean Architecture แยก Domain, Application และ Infrastructure เพื่อให้ business logic ไม่ผูกกับ framework หรือ database

**Speaker script:** Slide นี้ให้จำ direction ของ dependency ครับ Domain อยู่ในสุดและควรบริสุทธิ์ที่สุด Application หรือ service layer ใช้ domain เพื่อ implement use cases ส่วน Infrastructure เช่น database, external API, message queue และ web framework อยู่ข้างนอก ถ้าเรารักษา dependency ให้ไหลเข้าข้างใน code จะ test ง่าย เปลี่ยน adapter ง่าย และ AI จะ generate code ที่ไม่ปนกันมั่ว

### 6.2 TDD-First Development Cycle and PostToolUse Hook

**Key message:** TDD-first รวมกับ PostToolUse Hook ทำให้ทุก code change ถูก test ทันทีหลัง AI แก้ไฟล์

**Speaker script:** Cycle คือ write failing test, implement minimal code, run tests, refactor แล้ว repeat แต่ใน agentic workflow เราเพิ่ม PostToolUse Hook ให้รัน test อัตโนมัติหลัง AI แก้ code หรือ test file ผลคือ feedback มาเร็วมาก ถ้า test fail Claude ต้องแก้ต่อก่อนส่งงาน Human จึงไม่ต้องเป็นคนคอยบอกทุกครั้งว่า "รัน test แล้วหรือยัง" เพราะ workflow enforce ให้เอง

### 6.3 Five Channel Adapters, One Interface

**Key message:** Adapter pattern ทำให้หลาย channel ใช้ interface เดียวกัน และ core system ไม่ต้องรู้รายละเอียด channel

**Speaker script:** LINE, Facebook, Slack, WhatsApp และ Teams มี API ต่างกัน แต่ใน core system เราต้องการ behavior เดียว เช่น Receive, Normalize, Send หรือ VerifyWebhook เราจึงกำหนด interface กลาง แล้วให้แต่ละ adapter implement ตาม channel ของตัวเอง ข้อดีคือเพิ่ม channel ใหม่โดยไม่แก้ message router หลักมาก และ contract test สามารถ verify ได้ว่า adapter ทุกตัวทำตาม interface จริง

### 6.4 SMS Gateway Failover and Circuit Breaker

**Key message:** Circuit breaker และ provider failover ป้องกัน SMS failure ไม่ให้ลามเป็น system-wide outage

**Speaker script:** SMS provider อาจ timeout, rate limit หรือ outage ได้ เราจึงใช้ circuit breaker ตรวจ failure rate ถ้า provider หลักเริ่ม fail จะ open circuit และ failover ไป secondary provider แทน ระหว่างนั้นระบบอาจใช้ retry policy และ health check เพื่อดูว่า provider หลักกลับมาแล้วหรือยัง ประเด็นคือ reliability ไม่ได้มาจาก provider เดียวที่ดีที่สุด แต่มาจาก design ที่รับ failure ได้

### 6.5 Complete Developer Workflow Pipeline

**Key message:** Developer workflow ที่ดีเชื่อม architecture, implementation, tests, review และ PR เป็น pipeline เดียว

**Speaker script:** Slide นี้รวมภาพตั้งแต่ architecture ไปจนถึง pull request ครับ เริ่มจาก requirement และ design, เขียน test, implement code, run local checks, security review, CI pipeline และเปิด PR พร้อม review artifacts เมื่อ Claude Code ทำงานใน pipeline นี้ เราจะเห็นว่า AI ไม่ได้แค่สร้าง code snippet แต่ช่วยขับ workflow ทั้งหมดให้ครบก่อนส่งให้ human review

## Chapter 7

### 7.1 AI-Adjusted Testing Pyramid

**Key message:** เมื่อ AI เขียน code ได้เร็ว testing pyramid ต้องปรับให้เน้น safety net ที่คุ้ม risk มากที่สุด

**Speaker script:** Testing pyramid แบบเดิมยังใช้ได้ แต่ AI ทำให้ปริมาณ code และ change frequency เพิ่มขึ้น เราจึงต้องชัดว่า unit tests ครอบคลุม logic ที่เร็วและเยอะ, integration tests ตรวจ boundary กับ database, queue และ external services, ส่วน E2E tests ตรวจ critical user flows เท่านั้น อย่าให้ AI generate E2E จำนวนมากจนช้า แต่ให้ใช้ pyramid เพื่อ balance speed กับ confidence

### 7.2 Test Strategy Risk Matrix

**Key message:** เลือก test จาก risk โดยดู impact และ probability ไม่ใช่ test ทุกอย่างเท่ากัน

**Speaker script:** Risk matrix ช่วยตัดสินใจว่าควรลงทุน test ตรงไหนก่อนครับ Feature ที่ impact สูงและ probability สูงต้องมี automated tests แข็งแรง เช่น payment, message delivery หรือ auth ส่วน low impact และ low probability อาจใช้ lighter checks ได้ หลักคือ AI ทำ test ได้เร็วก็จริง แต่ strategy ยังต้องมาจากมนุษย์ เราต้องบอกว่า risk ไหนสำคัญกับ business

### 7.3 PostToolUse Auto-Test Feedback Loop

**Key message:** Auto-test loop ทำให้ AI ได้ feedback ทันทีและแก้ failure ใน session เดียว

**Speaker script:** หลัง Claude Code แก้ไฟล์ PostToolUse Hook จะรัน test ที่เกี่ยวข้อง ถ้า pass ก็ไปต่อ ถ้า fail ผลลัพธ์กลับเข้า session ให้ AI วิเคราะห์และแก้ต่อทันที Loop นี้ลดเวลาที่ human ต้อง copy paste error log ไปมา และทำให้ quality gate อยู่ใกล้กับจุดที่ code ถูกเปลี่ยนมากที่สุด ยิ่ง feedback เร็ว bug ยิ่งถูกแก้ถูกจุด

### 7.4 Integration Test Infrastructure with testcontainers-go

**Key message:** Testcontainers ช่วยให้ integration tests ใช้ real services เช่น MongoDB, Redis หรือ RabbitMQ ใน environment ที่ reproducible

**Speaker script:** Mock มีประโยชน์ แต่บาง bug จะเจอได้เมื่อคุยกับ service จริงเท่านั้น testcontainers-go ช่วย spin up container ของ MongoDB, Redis, RabbitMQ หรือ ClickHouse ระหว่าง test แล้ว tear down หลังจบ ทำให้ integration test ใกล้ production behavior มากขึ้นแต่ยัง reproducible เหมาะมากกับ agentic workflow เพราะ AI สามารถรัน test แล้วเห็น failure จาก infrastructure จริง

### 7.5 Contract Test Adapter Interface Verification

**Key message:** Contract tests ตรวจว่า adapter ทุกตัวทำตาม interface และ behavior ที่ core system คาดหวัง

**Speaker script:** เมื่อเรามีหลาย channel adapters ความเสี่ยงคือ adapter ตัวหนึ่ง normalize message ไม่เหมือนคนอื่น หรือ handle error ไม่ตรง contract Contract test จึงสร้าง shared test suite ที่ทุก adapter ต้องผ่าน เช่น input webhook ต้องกลายเป็น UnifiedMessage แบบเดียวกัน, invalid signature ต้องถูก reject, send failure ต้อง return error format เดียวกัน นี่คือ safety net ที่ป้องกัน integration break แบบเงียบ ๆ

## Chapter 8

### 8.1 Shared Git Worktrees

**Key message:** Git worktrees ทำให้หลาย Claude sessions ทำงานบน branch แยกพร้อมกันได้โดยไม่ชน working directory

**Speaker script:** ถ้าเปิด AI หลาย session ใน folder เดียวกัน โอกาสไฟล์ชนกันสูง Git worktree แก้ปัญหานี้โดยให้แต่ละ branch มี working directory ของตัวเอง เช่น feature A, test cleanup และ docs update ทำพร้อมกันได้ ทุก session มี repo เดียวกันแต่ checkout แยกกัน เมื่อเสร็จแล้วค่อย merge ผ่าน PR ตามปกติ นี่คือ foundation ของ parallel execution ที่ปลอดภัย

### 8.2 Six Week Wave Plan

**Key message:** Wave planning แบ่งงานเป็นช่วงที่ parallel ได้จริง และมี resync point ชัดเจน

**Speaker script:** Parallel work ต้องวางแผนเป็น wave ไม่ใช่ปล่อยทุกคนเริ่มพร้อมกันแบบไร้ลำดับ Wave แรกอาจเป็น research และ architecture, wave ถัดมาเป็น implementation, แล้วตามด้วย testing, hardening และ release แต่ละ wave ต้องมี artifact และ checkpoint เพื่อ resync ถ้า dependency ไม่ชัด งาน parallel จะกลายเป็น merge conflict และ rework

### 8.3 Sonnet Speed, Opus Depth

**Key message:** เลือก model ตามงาน: Sonnet สำหรับ speed และ routine work, Opus สำหรับ depth, risk และ reasoning

**Speaker script:** ไม่จำเป็นต้องใช้ model แพงที่สุดกับทุกงานครับ Sonnet เหมาะกับงานที่ต้องเร็ว เช่น scaffolding, docs, simple tests หรือ refactor ที่ scope ชัด ส่วน Opus เหมาะกับ architecture review, security analysis, incident reasoning หรือ decision ที่มี trade-offs เยอะ การเลือก model ให้ถูกช่วยคุม cost และ latency โดยยังได้ quality ที่เหมาะกับ risk ของงาน

### 8.4 Context Health Over Time

**Key message:** Context health ต้องถูกดูแลตลอด session ไม่เช่นนั้น AI จะเริ่มหลุดจาก requirement และ decision เดิม

**Speaker script:** Context window มีขีดจำกัดครับ ตอนต้น session AI เห็นข้อมูลครบ แต่เมื่อ conversation ยาวขึ้น context อาจเต็มหรือมี noise มากขึ้น วิธีดูแลคือสรุป decision สำคัญ, เก็บ artifact ลงไฟล์, update CLAUDE.md หรือ role notes เมื่อมี convention ใหม่ และเริ่ม session ใหม่เมื่อ context เสื่อมมาก อย่าปล่อยให้ AI ทำงานยาวโดยไม่มี memory hygiene

### 8.5 Parallel PR CI Timeline

**Key message:** Parallel PRs ต้องมี CI timeline และ merge discipline เพื่อไม่ให้ changes ชนกันตอนท้าย

**Speaker script:** เมื่อหลาย worktrees สร้าง PR พร้อมกัน CI จะกลายเป็น coordination point ครับ เราต้องดูว่า PR ไหน independent, PR ไหนต้อง merge ก่อน, และต้อง rebase หรือ rerun CI หลัง base branch เปลี่ยนไหม Timeline นี้ช่วยให้ team เห็นว่า parallel execution ไม่ได้จบตอน code เสร็จ แต่ต้องรวมถึง review, CI, conflict resolution และ merge order ด้วย
