# สคริปต์สอน — AI Agentic SDLC (ภาษาไทย)
> โทน: ผ่อนคลาย · ใช้งานได้จริง · เหมือนคุยกับเพื่อน
> รูปแบบ: Outline + ประเด็นหลักแต่ละบท

---

## เปิดคอร์ส (Course Intro)

**Hook:**
> "ถามตรงๆ เลยนะ — ที่ทำงานของเราตอนนี้ใช้ AI ช่วย code ไหม? ถ้าใช้อยู่แล้ว เราจะทำให้มันทำงานแทนทั้ง team ได้ — ถ้ายังไม่ใช้ หลังจบคอร์สนี้จะกลับไปทำงานแบบเดิมไม่ได้อีกแล้ว"

**บอก context:**
- คอร์สนี้ไม่ได้สอน AI ทั่วไป — สอน **วิธีสร้าง software จริงๆ ด้วย AI agent**
- project ที่ใช้เป็นตัวอย่างตลอดคอร์ส: ระบบส่งข้อความ multi-channel (เหมือน platform จริงในบริษัท)
- เรียนจบแล้วได้อะไร: workflow ที่ AI ทำงานแทนได้ตั้งแต่ เขียน spec → code → test → deploy

---

## Part 1: Foundations (บทที่ 1–8)

---

### บทที่ 1 — AI-Augmented SDLC

**ประเด็นหลัก:**
- SDLC แบบเดิม vs แบบ Agentic ต่างกันยังไง — วาด timeline ให้เห็น
- ใน team มี role อะไรบ้าง และ AI เข้ามาแทน/ช่วย role ไหน
- หลักการพัฒนาแบบ Agentic 4 ข้อที่ต้องจำ

**ของให้ลอง:**
- ให้ผู้เรียนลองนึกดูว่างานที่ทำอยู่ทุกวัน ขั้นตอนไหนที่ AI น่าจะช่วยได้มากที่สุด

**Key takeaway:**
> "Agentic SDLC ไม่ใช่แค่ใช้ AI เขียน code — มันคือการออกแบบ workflow ให้ AI เป็นส่วนหนึ่งของ team จริงๆ"

---

### บทที่ 2 — Claude Code Setup

**ประเด็นหลัก:**
- Permission mode มีกี่แบบ เลือกใช้แบบไหนตอนไหน (อย่าตั้ง yolo ตั้งแต่วันแรก)
- `CLAUDE.md` คือ "รัฐธรรมนูญ" ของโปรเจกต์ — บอก AI ว่าทำอะไรได้ ไม่ได้
- Role file inheritance — แชร์ rule ข้าม project ยังไง
- MCP Server ecosystem — ต่อ Claude เข้ากับ tool อื่นๆ
- Checklist setup workspace ที่ดี

**ของให้ลอง:**
- สร้าง `CLAUDE.md` ไฟล์แรกของตัวเอง — เขียนแค่ 5 rule ก็พอ

**Key takeaway:**
> "`CLAUDE.md` ที่ดีประหยัดเวลาได้มากกว่า prompt ยาวๆ เพราะ AI อ่านทุกครั้งที่เริ่มงาน"

---

### บทที่ 3 — Hooks & Skills

**ประเด็นหลัก:**
- Hook คืออะไร — เปรียบเหมือน middleware ของ AI (ยิง script ก่อน/หลัง tool ทำงาน)
- 4 ประเภท Hook: PreToolUse · PostToolUse · Stop · Notification
- Exit code 0 vs 2 — allow vs block
- Skill = slash command ที่เราเขียนเอง เก็บใน `.claude/skills/`
- Subagent คืออะไร — Claude instance แยก ทำงานพร้อมกันได้

**ของให้ลอง:**
- เขียน hook ง่ายๆ ที่ block `rm -rf` ก่อนจะรัน
- ลองเขียน skill `/daily-standup` สำหรับ generate standup report

**Key takeaway:**
> "Hook = guard · Skill = shortcut · Subagent = ลูกน้อง — จำสามอย่างนี้ก็เข้าใจบท 3 แล้ว"

---

### บทที่ 4 — Prompt Engineering

**ประเด็นหลัก:**
- Framework RISEN: Role · Instructions · Steps · Expectations · Narrowing
- PRD generation workflow 3 phase — ไม่ต้องนั่งเขียน spec เองทั้งหมด
- User Story anatomy — เขียนยังไงให้ AI ทำต่อได้เลย
- Sprint Backlog dependency graph — จัดลำดับงานไม่ให้ติดกัน
- `/sprint-plan` skill cycle — จาก backlog → assigned tasks อัตโนมัติ

**ของให้ลอง:**
- เอา feature จริงในงานมาเขียน prompt ด้วย RISEN แล้วเปรียบเทียบผลลัพธ์กับ prompt ปกติ

**Key takeaway:**
> "Prompt ที่ดีไม่ใช่ prompt ที่ยาว — แต่เป็น prompt ที่บอก role + context + constraint ครบ"

---

### บทที่ 5 — System Architecture

**ประเด็นหลัก:**
- Message queue topology — fanout exchange ทำงานยังไง (ไม่ต้องรู้ tech stack เฉพาะ รู้ concept พอ)
- Unified data schema — ออกแบบ schema ที่รองรับหลาย channel พร้อมกัน
- Caching layer — cache 2 บทบาท: speed + state
- Analytics pipeline — data ไหลจาก message ถึง dashboard ยังไง
- ADR (Architecture Decision Record) — บันทึกเหตุผลการตัดสินใจ ไม่ใช่แค่ผลลัพธ์

**ของให้ลอง:**
- ลองเขียน ADR 1 อัน จากการตัดสินใจ tech ที่เคยทำในโปรเจกต์ตัวเอง

**Key takeaway:**
> "Architecture ที่ดีอธิบายได้ว่า 'ทำไม' ไม่ใช่แค่ 'ทำอะไร' — ADR คือเครื่องมือนั้น"

---

### บทที่ 6 — TDD & Clean Architecture

**ประเด็นหลัก:**
- Clean Architecture 3 layer — Domain · Application · Infrastructure ห้ามสลับกัน
- TDD-First cycle กับ PostToolUse hook — เขียน test ก่อน แล้วให้ hook รันอัตโนมัติ
- Adapter pattern — 1 interface หลาย implementation เปลี่ยน channel ไม่ต้อง refactor core
- Circuit breaker — failover ยังไงให้ระบบไม่ล่มทั้งก้อน
- Dev workflow pipeline — ตั้งแต่ code ถึง PR ใน 1 กระบวนการ

**ของให้ลอง:**
- วาด 3 layer ของโปรเจกต์ตัวเองดู — แล้วดูว่า dependency ไหลถูกทางไหม

**Key takeaway:**
> "Clean Architecture ไม่ใช่เรื่อง folder structure — มันเรื่องทิศทางของ dependency"

---

### บทที่ 7 — Testing Strategy

**ประเด็นหลัก:**
- AI-Adjusted Testing Pyramid — สัดส่วน unit/integration/e2e เปลี่ยนยังไงเมื่อมี AI เขียน code
- Risk matrix — ตัดสินใจว่า test อะไรก่อนโดยดูจาก impact × probability
- PostToolUse hook auto-test — ทุกครั้งที่ AI แก้ไฟล์ test รันเองเลย
- Integration test กับ Testcontainers — test กับ service จริง ไม่ใช่ mock
- Contract test — ตรวจ interface ระหว่าง service ไม่ให้ break กันเงียบๆ

**ของให้ลอง:**
- ดู test suite ที่มีอยู่ แล้วลอง map ว่าอยู่ระดับไหนใน pyramid

**Key takeaway:**
> "AI เขียน test ได้เร็ว แต่เราต้องออกแบบ strategy ว่าจะ test อะไร — นั่นยังเป็นงานของคน"

---

### บทที่ 8 — Parallel Execution & Worktrees

**ประเด็นหลัก:**
- Git Worktree — รัน Claude หลาย instance บน branch แยก พร้อมกัน ไม่ conflict
- 6-Week wave plan — วางแผนงานเป็น wave ให้ parallel ได้จริง
- Speed vs Depth trade-off — เลือก model ให้ตรงงาน ไม่ใช่ใช้ตัวแพงเสมอ
- Context health — context window เต็มแล้วทำไง ดูแลยังไงให้ไม่เสีย
- Parallel PR & CI — หลาย PR รัน CI พร้อมกัน merge ยังไงไม่ให้งานชน

**ของให้ลอง:**
- ลอง `git worktree add` แล้วเปิด Claude 2 terminal พร้อมกัน

**Key takeaway:**
> "Parallel execution ไม่ใช่แค่เรื่อง AI — มันเรื่อง Git workflow ที่ต้องออกแบบมาก่อน"

---

## Part 2: Production & Scale (บทที่ 9–15)

---

### บทที่ 9 — CI/CD & Deployment

**ประเด็นหลัก:**
- Pipeline เริ่มตั้งแต่ PR สร้าง — ไม่ใช่แค่ตอน merge
- Container service topology — service ต่อกันยังไงใน environment จริง
- Multi-stage build — build image ให้เล็ก ปลอดภัย เร็ว
- Blue-Green deployment — switch traffic โดยไม่มี downtime
- Deploy workflow — ขั้นตอนจาก staging → production

**Key takeaway:**
> "CI/CD ที่ดีทำให้ deploy น่าเบื่อ — เพราะมันทำเองได้ ไม่มีดราม่า"

---

### บทที่ 10 — Production Launch

**ประเด็นหลัก:**
- Production readiness scorecard — checklist ก่อน go-live
- Launch day timeline — ใครทำอะไรตอนไหน
- Load test targets — ตั้ง threshold จาก business requirement ไม่ใช่เดาเอา
- Production dashboard — metric อะไรต้องดูตลอดวันแรก
- Sprint improvement cycle — หลัง launch ไม่ใช่จบ แต่เริ่มวน

**Key takeaway:**
> "Launch day ที่ดีคือ launch day ที่น่าเบื่อ — เพราะทุกอย่างผ่าน checklist มาแล้ว"

---

### บทที่ 11 — Observability

**ประเด็นหลัก:**
- 3 pillars: Logs · Metrics · Traces — ต่างกันอย่างไร ใช้เมื่อไหร่
- Four Golden Signals: Latency · Traffic · Errors · Saturation — จำ 4 ตัวนี้ไว้ดู production
- Error budget — SLO คืออะไร budget หมดแล้วทำยังไง
- Alert noise reduction — alert เยอะไม่ใช่ดี ต้องกรองให้เหลือแค่ที่ actionable
- Trace waterfall — ดู request เดินทางผ่าน service ไหนบ้าง

**Key takeaway:**
> "Observability ไม่ใช่เรื่อง tool — เป็นเรื่องว่าเราตอบคำถาม 'ระบบป่วยที่ไหน' ได้เร็วแค่ไหน"

---

### บทที่ 12 — Incident Response & Retrospectives

**ประเด็นหลัก:**
- Incident lifecycle 5 phase: Detect → Triage → Mitigate → Resolve → Review
- Blameless post-mortem — หา root cause ไม่ใช่หาคนผิด
- Retrospective data collection — เก็บข้อมูลยังไงให้ retro มีคุณภาพ
- AI Impact Scorecard — วัดผลว่า AI ช่วยได้จริงแค่ไหน เป็น data ไม่ใช่ความรู้สึก
- CLAUDE.md evolution — file นี้ควรเปลี่ยนตามที่ team เรียนรู้

**Key takeaway:**
> "Incident ที่ดีที่สุดคือ incident ที่เกิดแล้วทำให้ระบบแข็งแกร่งขึ้น ไม่ใช่แค่แก้แล้วลืม"

---

### บทที่ 13 — Clean Architecture (เชิงลึก)

**ประเด็นหลัก:**
- Standard project layout — โครงสร้าง folder ที่ทีมเข้าใจตรงกัน
- Dependency ring — วงแหวน dependency ต้องไหลทางเดียว (inward)
- Dependency injection wiring — ต่อ component เข้าหากันที่ entry point เดียว
- Config resolution order — ลำดับที่ config ถูกโหลด env → file → default
- Anti-patterns — ของที่ควรหลีกเลี่ยง เทียบกับ clean version ให้เห็นชัด

**Key takeaway:**
> "Architecture ที่ดีทำให้คนใหม่เปิด codebase แล้วรู้ว่าต้องแก้ที่ไหน ภายใน 10 นาที"

---

### บทที่ 14 — Role-Based Subagents

**ประเด็นหลัก:**
- Human role vs Agent role vs Skill — แต่ละอย่างรับผิดชอบอะไร
- File ownership map — agent ไหนแตะไฟล์ไหนได้ ป้องกัน conflict
- 4 workflow modes: Sync · Async · Parallel · Resync — เลือกใช้ตามสถานการณ์
- Parallel wave → resync — ส่งงานพร้อมกัน แล้วรวมผลยังไง
- Coordination rules vs pitfalls — 7 กฎที่ต้องตาม vs罠ที่ต้องหลีกเลี่ยง

**Key takeaway:**
> "Subagent ทำงานได้ดีก็ต่อเมื่อมี boundary ชัดเจน — ไม่งั้นก็แค่ chaos แบบเร็วขึ้น"

---

### บทที่ 15 — Agent Team Model

**ประเด็นหลัก:**
- 8-agent team roster — แต่ละ agent มี persona ชัดเจน เหมือน team member จริง
- Agent team vs role-based subagents — ต่างกันยังไง เลือกแบบไหนเมื่อไหร่
- 9-step agent delivery flow — ตั้งแต่รับ requirement ถึง deliver
- Charter + Team State + Handoff Packet — 3 artifact ที่ทำให้ agent ทำงานต่อกันได้
- 6 guardrails vs 7 pitfalls — ของที่ต้องตั้ง vs ความผิดพลาดที่เจอบ่อย

**Key takeaway:**
> "Agent team ไม่ใช่แค่ automation — มันคือการออกแบบ organization ใหม่ที่มี AI เป็นสมาชิก"

---

## ปิดคอร์ส (Course Outro)

**สรุปภาพรวม:**
- Part 1 สร้าง foundation: setup · hooks · skills · architecture · testing · parallel work
- Part 2 ขึ้น production จริง: deploy · observability · incident · scale ด้วย agent

**Call to action:**
> "อย่าเพิ่งรู้สึกว่าต้องทำครบทุกอย่างพร้อมกัน — เลือก 1 อย่างที่เอาไปใช้ได้พรุ่งนี้เลย แล้วค่อยๆ build ขึ้นมา"

**ทิ้งท้าย:**
> "Software development กำลังเปลี่ยนไป ไม่ใช่เพราะ AI똑똑กว่าเรา — แต่เพราะเรารู้จักใช้มันเป็น นั่นแหละคือ skill ที่แยก senior ออกจากคนอื่นในยุคนี้"

---

*หมายเหตุสำหรับผู้สอน: แต่ละบทมีเวลาประมาณ 20–30 นาที รวมส่วน demo และ Q&A สั้นๆ ท้ายบท*
