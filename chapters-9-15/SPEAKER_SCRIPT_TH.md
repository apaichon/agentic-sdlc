# Speaker Script TH - Chapters 9-15

รูปแบบ: `Key message` คือประเด็นที่ผู้เรียนต้องจำจาก slide นั้น และ `Speaker script` คือสคริปต์พูดภาษาไทย โดยคง technical words สำคัญเป็น English

## Chapter 9

### 9.1 PR Created CI/CD Pipeline

**Key message:** CI/CD ควรเริ่มตั้งแต่ PR ถูกสร้าง ไม่ใช่รอ merge แล้วค่อยตรวจ

**Speaker script:** Slide นี้ให้มอง PR เป็น trigger แรกของ delivery pipeline ครับ เมื่อ PR ถูกสร้าง ระบบควรรัน lint, unit tests, integration tests, security scan และ build image ทันที ผลลัพธ์เหล่านี้เป็น feedback ให้ Developer และ Reviewer ก่อน merge ถ้าเรารอให้ตรวจหลัง merge ความเสี่ยงจะย้ายไปอยู่ปลายทาง จุดสำคัญคือ PR ไม่ใช่แค่ discussion thread แต่เป็น quality gate แรกของ production workflow

### 9.2 Docker Compose Service Topology

**Key message:** Docker Compose ทำให้เห็น service topology ของระบบจริงใน local หรือ staging environment

**Speaker script:** ระบบ multi-channel messaging ไม่ได้มีแค่ app ตัวเดียว แต่มี Go API, adapters, RabbitMQ, MongoDB, Redis, ClickHouse และ frontend Docker Compose ช่วยประกาศ network, ports, dependencies และ environment variables ให้รัน stack ใกล้ production ได้ง่ายขึ้น สำหรับ AI workflow สิ่งนี้สำคัญเพราะ Claude Code และ tests สามารถอ้างอิง topology เดียวกัน ไม่ต้องเดาว่า service ไหนต่อกับอะไร

### 9.3 Multi-Stage Docker Build

**Key message:** Multi-stage Docker build แยก build environment ออกจาก runtime image เพื่อให้ image เล็ก ปลอดภัย และ deploy เร็ว

**Speaker script:** Build stage มี compiler, dependency tools และ test utilities ได้ แต่ runtime stage ควรมีเฉพาะ binary และไฟล์จำเป็นเท่านั้น เทคนิคนี้ลด image size, ลด attack surface และทำให้ pull image เร็วขึ้น ใน Go service pattern ที่พบบ่อยคือ stage แรกใช้ golang image build binary แล้ว stage สุดท้ายใช้ distroless หรือ alpine เพื่อรัน binary นั้น

### 9.4 Blue-Green Deployment Switch

**Key message:** Blue-Green Deployment ลด downtime โดยเตรียม environment ใหม่ให้พร้อมก่อน switch traffic

**Speaker script:** Blue environment คือ production ปัจจุบัน ส่วน Green คือ version ใหม่ที่ deploy และ health check ไว้ก่อน เมื่อ Green พร้อม เราค่อย switch traffic จาก Blue ไป Green ผ่าน load balancer หรือ router ถ้าเจอปัญหาสามารถ rollback กลับ Blue ได้เร็ว ข้อดีคือ deploy กลายเป็น traffic switch ไม่ใช่การแก้ระบบ production กลางอากาศ

### 9.5 Deploy Production Workflow

**Key message:** Production deploy ต้องมี staging validation, approval gate, rollout, monitoring และ rollback path

**Speaker script:** Workflow ที่ดีเริ่มจาก artifact เดียวกันผ่าน staging, รัน smoke tests และ health checks, ขอ human approval เมื่อ risk สูง, deploy production แบบ controlled rollout, แล้ว monitor golden signals หลัง release ถ้า metric แย่ต้องมี rollback path ที่ชัดเจน จุดสำคัญคือ deploy ไม่ใช่ command เดียว แต่เป็น process ที่รวม validation และ decision gate

## Chapter 10

### 10.1 Production Readiness Scorecard

**Key message:** Readiness scorecard เปลี่ยนคำถาม "พร้อม launch ไหม" ให้เป็น checklist ที่วัดได้

**Speaker script:** ก่อน go-live เราต้องตรวจหลายมิติ เช่น functionality, performance, security, observability, runbooks, backup, rollback และ support readiness Scorecard ช่วยให้ทีมเห็น item ที่ pass, warning หรือ fail อย่างชัดเจน ถ้าบางเรื่องยังแดง เช่น no rollback plan หรือ alert ยังไม่พร้อม ก็ไม่ควร launch เพราะ production readiness ต้องอิง evidence ไม่ใช่ความรู้สึก

### 10.2 Launch Day Timeline

**Key message:** Launch day ต้องมี timeline, owner และ checkpoint เพื่อให้ทุกคนรู้ว่าต้องทำอะไรเมื่อไร

**Speaker script:** Launch ที่ดีควรถูก script ไว้ล่วงหน้าครับ เช่น freeze changes, final smoke test, enable feature flag, ramp traffic, monitor dashboard, check support channel และ confirm go/no-go แต่ละช่วงต้องมี owner ชัดเจน ไม่ใช่ทุกคนดูทุกอย่างพร้อมกัน Timeline ทำให้วัน launch น่าเบื่อ ซึ่งเป็นเรื่องดี เพราะ surprise ใน production มักแปลว่าเราเตรียมไม่พอ

### 10.3 Load Test Target

**Key message:** Load test target ต้องมาจาก business requirement และ SLO ไม่ใช่ตัวเลขที่เดาเอง

**Speaker script:** ถ้าระบบต้องรองรับ 10K messages per second หรือ P95 latency ต่ำกว่า 200ms เราต้องแปลง requirement เหล่านี้เป็น load test scenario ที่วัดได้ เช่น throughput, latency, error rate และ saturation Load test ไม่ใช่แค่ยิง request เยอะ ๆ แต่ต้องจำลอง traffic pattern ที่ใกล้จริง เช่น burst จาก campaign หรือ peak hour ของ chat traffic

### 10.4 Production Dashboard

**Key message:** Dashboard ที่ดีต้องตอบได้เร็วว่าระบบ healthy ไหม และปัญหาอยู่ layer ไหน

**Speaker script:** Production dashboard ควรแสดง metric ที่ actionable เช่น message throughput, P95 latency, error rate by channel, queue depth, database health และ deployment status ไม่ใช่ใส่ chart ให้เยอะที่สุด เป้าคือเมื่อ incident เกิด ทีมต้องรู้ว่า bottleneck อยู่ที่ adapter, RabbitMQ, database, API หรือ notification layer ภายในไม่กี่นาที

### 10.5 Sprint Improvement Cycle

**Key message:** หลัง launch ต้องเอาข้อมูล production กลับไปปรับ sprint process อย่างต่อเนื่อง

**Speaker script:** Launch ไม่ใช่จุดจบครับ หลัง release เราควรเก็บ incident metrics, user feedback, velocity, escaped defects และ AI usage patterns แล้วนำเข้าวงจร retrospective เพื่อปรับ CLAUDE.md, skills, tests, runbooks และ backlog รอบถัดไป นี่คือ continuous improvement ที่ทำให้ Agentic SDLC แข็งแรงขึ้นเรื่อย ๆ ไม่ใช่แค่ส่ง feature ให้เร็วขึ้น

## Chapter 11

### 11.1 Observability Pillars

**Key message:** Logs, Metrics และ Traces ตอบคำถามคนละแบบ แต่ต้องใช้ร่วมกันเพื่อ debug production

**Speaker script:** Metrics บอกว่าเกิดอะไรขึ้นในภาพรวม เช่น latency สูงหรือ error rate เพิ่ม Logs บอก event รายละเอียด เช่น request ไหน fail และ error message คืออะไร Traces บอก request เดินทางผ่าน service ไหนและใช้เวลาตรงไหนนาน เมื่อรวมสาม pillar นี้เข้าด้วยกัน เราจะตอบได้ทั้ง what, why และ where ของปัญหา production

### 11.2 Four Golden Signals Light

**Key message:** Four Golden Signals คือ Latency, Traffic, Errors และ Saturation สำหรับดู health ของ service

**Speaker script:** ถ้าจำ observability metric ไม่หมด ให้จำ 4 ตัวนี้ครับ Latency คือ service ช้าแค่ไหน Traffic คือรับ load เท่าไร Errors คือ fail กี่เปอร์เซ็นต์ และ Saturation คือ resource ใกล้เต็มหรือยัง เช่น CPU, memory, queue depth หรือ connection pool สัญญาณทั้งสี่ช่วยให้เรารู้ว่าระบบกำลังป่วยแบบไหน

### 11.3 Four Golden Signals Dark

**Key message:** Dark theme slide สื่อ message เดียวกัน: ใช้ Golden Signals เป็น dashboard หลักสำหรับ production

**Speaker script:** Slide นี้เป็น visual variant ของ Four Golden Signals ครับ เนื้อหายังคือ Latency, Traffic, Errors และ Saturation เวลาสอนให้ย้ำว่า dashboard ที่ดีไม่ต้องเริ่มจาก metric เป็นร้อยตัว แต่เริ่มจากสี่ signal นี้ก่อน แล้วค่อย drill down ไปยัง service-specific metrics เมื่อ signal ใด signal หนึ่งผิดปกติ

### 11.4 Error Budget Light

**Key message:** Error budget แปลง SLO เป็นเวลาที่ระบบยอม fail ได้ และใช้ตัดสินใจว่าจะ ship feature หรือ fix reliability

**Speaker script:** ถ้า SLO คือ 99.9% ใน 30 วัน error budget คือประมาณ 43.2 minutes ของ downtime หรือ bad experience ที่ยอมรับได้ ถ้า budget เหลือเยอะ เราอาจ deploy feature ได้ aggressive ขึ้น แต่ถ้า burn rate สูงหรือ budget ต่ำกว่า threshold ทีมควร freeze feature แล้ว focus reliability Error budget ทำให้ product และ engineering คุยกันด้วยตัวเลขเดียวกัน

### 11.5 Error Budget Dark

**Key message:** Error budget dashboard ต้องแสดง remaining budget, status และ burn rate ให้ตัดสินใจได้ทันที

**Speaker script:** Version นี้เน้นการอ่าน dashboard ครับ ดู SLO target ของแต่ละ capability เช่น Message Delivery, API Latency และ SMS Delivery แล้วดู remaining budget ถ้ายังมากกว่า 50% อาจ ship features ต่อได้ แต่ถ้า budget ถูกใช้เร็วเกินไปต้อง investigate Burn rate สำคัญเพราะ budget 50% ที่ถูกใช้ในวันเดียวต่างจาก 50% ที่ใช้ตลอดเดือนมาก

### 11.6 Alert Noise Reduction Pipeline Light

**Key message:** Alert ที่ดีต้องถูก deduplicate, group by service, route by severity และ suppress ตอน maintenance

**Speaker script:** Alert เยอะไม่ได้แปลว่า observability ดีครับ ตัวอย่างนี้เริ่มจาก raw alerts จำนวนมาก แล้วลด noise ด้วยการ deduplicate alert ซ้ำจากหลาย pods, group ตาม service เช่น Message Router หรือ MongoDB, route ตาม severity ไป PagerDuty, Slack หรือ Grafana และ suppress non-critical alerts ระหว่าง maintenance เป้าคือให้ on-call เห็น alert ที่ actionable จริง ๆ

### 11.7 Alert Noise Reduction Pipeline Dark

**Key message:** Pipeline ลด alert noise จาก raw alerts ไปเป็น service groups และ routed alerts ที่ actionable

**Speaker script:** Slide นี้ใช้ตัวเลขให้เห็น impact ครับ จาก 47 raw alerts หลัง dedup อาจเหลือ 18 และ group เป็น 5 service groups ก่อน route เป็น critical, warning และ info Critical ต้อง page ทันที Warning อาจเป็น digest 15 นาที ส่วน Info review วันถัดไป หลักคือ priority ต้อง match response channel ไม่อย่างนั้นทีมจะ ignore alert เพราะเสียงดังเกินไป

### 11.8 Trace Waterfall Light

**Key message:** Trace waterfall ชี้ bottleneck ของ request ได้จาก span duration ในแต่ละ service

**Speaker script:** ตัวอย่าง trace นี้มี total 178ms และแบ่ง span เช่น line-adapter.Receive, router.Route, persistence.Save, analytics.Ingest และ notification.Push เมื่อดู waterfall จะเห็น bottleneck คือ FCM.Push ใช้ 53ms ใน notification path Trace ช่วยให้เราไม่ต้องเดาว่าช้าตรงไหน เพราะเห็น timing ของแต่ละ service และ sub-operation ชัดเจน

### 11.9 Trace Waterfall Dark

**Key message:** Trace waterfall ช่วยแยก latency contribution ของแต่ละ span แม้ใน distributed system

**Speaker script:** Version นี้เป็น theme อีกแบบของ trace เดิมครับ เวลาอธิบายให้ชี้ว่า request หนึ่งอาจผ่านหลาย service แต่ trace id เดียวกันเชื่อมทุก span เข้าด้วยกันได้ ถ้า latency สูง เราดูได้ทันทีว่าเกิดจาก validation, publish queue, database insert, analytics ingest หรือ push notification จุดนี้คือพลังของ distributed tracing

## Chapter 12

### 12.1 Five-Phase Incident Response Lifecycle

**Key message:** Incident response ต้องไหลผ่าน Detect, Triage, Mitigate, Resolve และ Post-Mortem พร้อมเวลาคาดหวังแต่ละ phase

**Speaker script:** Lifecycle นี้เริ่มจาก Detect ผ่าน alerts หรือ customer reports ต่อด้วย Triage เพื่อประเมิน severity และ blast radius จากนั้น Mitigate เช่น rollback, scale หรือ failover แล้ว Resolve ด้วย root cause fix จน SLO กลับมา สุดท้ายต้องมี Post-Mortem แบบ blameless เพื่อสร้าง action items จุดสำคัญคือ incident ไม่จบตอน service กลับมา แต่จบเมื่อเราเรียนรู้และป้องกันรอบหน้าได้

### 12.2 Blameless Post-Mortem Structure

**Key message:** Post-Mortem ที่ดีมี 7 sections และใช้ AI ช่วย draft ได้ แต่ human ต้องรับผิดชอบ learning และ action items

**Speaker script:** โครงสร้างมี Summary, Impact, Timeline, Root Cause, Contributing Factors, Action Items และ Lessons Learned Claude Code ช่วย draft summary, timeline, root cause analysis และ action items จาก logs หรือ incident notes ได้ แต่คำว่า blameless สำคัญมาก เราไม่ได้หาคนผิด เราหา system conditions ที่ทำให้ incident เกิดและทำให้ detection หรือ recovery ช้า

### 12.3 Retrospective Data Collection and Analysis Workflow

**Key message:** Retrospective ต้องใช้ data จาก incident metrics, velocity, AI usage และ team feedback แล้วแปลงเป็น action

**Speaker script:** Retro ที่ดีไม่ใช่แค่ถามว่ารู้สึกยังไง แต่รวบรวม data หลายแหล่ง เช่น MTTR, sprint velocity, cycle time, AI sessions, hooks, survey และ friction points จากนั้น analyze trend, recurring pattern และ AI impact แล้วออก action เช่น process changes, skill updates, CLAUDE.md refinements หรือ training needs สุดท้ายต้อง measure impact รอบถัดไป

### 12.4 AI Impact Scorecard Q2 2026

**Key message:** AI adoption ต้องวัดด้วย metric เช่น velocity, review turnaround, coverage, deployment frequency, MTTR และ ROI

**Speaker script:** Scorecard นี้เปรียบเทียบ before AI กับ after AI เช่น sprint velocity เพิ่ม, code review turnaround ลด, test coverage เพิ่ม, deployment frequency เพิ่ม, MTTD และ MTTR ลด รวมถึง developer satisfaction และ tooling cost สิ่งสำคัญคืออย่าอ้างว่า AI ช่วยจากความรู้สึกอย่างเดียว ให้วัด productivity gain และ ROI เป็นตัวเลขเพื่อคุยกับ leadership ได้

### 12.5 CLAUDE.md Evolution Over Time

**Key message:** CLAUDE.md ต้อง evolve จาก team learning, incidents และ retrospectives ไม่ใช่เขียนครั้งเดียวแล้วทิ้งไว้

**Speaker script:** Q1 อาจเริ่มจาก convention พื้นฐาน เช่น clean architecture และ table-driven tests พอเจอ production incidents ใน Q2 ก็เพิ่ม provider status checks, post-mortem rules หรือ retry limits Q3 หลัง retrospective อาจเพิ่ม incident-response skill, failover rules และ Testcontainers requirement พอ Q4 team mature ก็มี knowledge base ที่ละเอียดขึ้น CLAUDE.md จึงเป็น living document ของทีม

## Chapter 13

### 13.1 Standard Go Project Layout Tree

**Key message:** Go project layout ที่ชัดช่วยให้ AI และ human รู้ boundary ของ cmd, internal, domain, services, adapters และ pkg

**Speaker script:** Layout นี้เริ่มจาก cmd สำหรับ application entry points เช่น gateway/main.go, internal สำหรับ private business logic, domain สำหรับ entities, services สำหรับ use cases, repository interface และ adapters สำหรับ channel integrations เช่น LINE หรือ WhatsApp เมื่อ folder boundary ชัด AI จะวาง code ถูกที่มากขึ้น และ reviewer ตรวจได้ง่ายว่า dependency หรือ responsibility หลุด layer หรือไม่

### 13.2 Clean Architecture Dependency Ring

**Key message:** Dependency rule คือ arrows always point inward: outer layers depend on inner layers, never reverse

**Speaker script:** ด้านนอกคือ Handler เช่น HTTP, gRPC หรือ CLI ถัดเข้าไปคือ Service หรือ use cases จากนั้นเป็น Repository และ Adapter Interfaces และในสุดคือ Domain entities กับ value objects MongoDB, Redis, LINE API และ WhatsApp API อยู่ชั้นนอก เป็น concrete implementation ที่เสียบผ่าน interface เท่านั้น ถ้า domain import database driver แปลว่า architecture เริ่มผิดทิศ

### 13.3 Dependency Injection Wiring Sequence

**Key message:** main.go เป็น composition root ที่รู้ concrete types ทั้งหมด และ inject interface เข้า service

**Speaker script:** Wiring sequence เริ่มจาก load config ด้วย Viper, connect MongoDB, สร้าง mongorepo ที่ satisfy MessageRepository interface, สร้าง channel adapters เช่น line.New และ whatsapp.New, สร้าง service โดยรับ interface ไม่ใช่ concrete type แล้วค่อยสร้าง handler และ start server ข้อสำคัญคือ only main.go knows concrete types ส่วน business layer เห็นแค่ abstractions ทำให้ test และ replacement ง่าย

### 13.4 Viper Config Four-Step Resolution Order

**Key message:** Config resolution ต้องมี priority ชัด โดย environment variables ควร override defaults และ config file

**Speaker script:** Viper config flow เริ่มจาก compiled defaults ที่ priority ต่ำสุด เช่น port 8080 จากนั้น config.yaml override ค่า default บางส่วน และ environment variables override ได้สูงสุด เช่น CONSOLIDATE_SERVER_PORT=9000 ข้อดีคือ deploy environment เปลี่ยน config ได้โดยไม่ rebuild image และเราสามารถ fail fast เมื่อ required config เช่น Mongo URI หายไป

### 13.5 Anti-Patterns vs Clean Architecture

**Key message:** Clean Architecture แก้ anti-patterns เช่น god package, import cycle และ concrete dependency ด้วย boundaries และ interface inversion

**Speaker script:** ฝั่ง anti-pattern มี code ทุกอย่างอยู่ก้อนเดียว ทำให้ tight coupling และเปลี่ยนยาก มี import cycle ที่ทำให้ build fail และ service ผูกกับ concrete repository โดยตรง ฝั่ง clean solution แก้ด้วย standard layout, acyclic dependencies และ interface inversion เช่น service depends on interface ส่วน repo implement interface จากด้านนอก หลักคือ refactor เพื่อให้ change localized และ testable

## Chapter 14

### 14.1 Human Role, Agent Role, Skill Taxonomy

**Key message:** Human owns decisions, Agent produces artifacts, Skill defines reusable capability

**Speaker script:** Taxonomy นี้แยก 3 ชั้นครับ Human Role รับผิดชอบ outcome, context และ decision Agent Role ทำ task, produce artifact และ surface options ส่วน Skill คือ capability เฉพาะ เช่น requirement-refinement หรือ design-review ตัวอย่าง PM human กำหนด goal และ trade-offs, PM Agent draft requirements, และ skill ช่วย refine user stories วิธีคิดนี้ช่วยไม่ให้เราสับสนว่า AI รับผิดชอบผลลัพธ์แทนคน

### 14.2 File Ownership Map

**Key message:** Same-repo multi-agent work ต้องมี file ownership map เพื่อหลีกเลี่ยง merge conflicts และ responsibility overlap

**Speaker script:** Slide นี้ระบุว่า Team Lead หรือ CLAUDE.md owns project-wide context, PM Agent owns docs/product, Architect Agent owns docs/architecture, Developer Agent owns internal, Tester Agent owns tests และ DevOps Agent owns .github/workflows Solid arrow คือ primary owner ส่วน dashed arrow คือช่วยได้ แต่ไม่ใช่เจ้าของหลัก กฎนี้สำคัญมากเมื่อมีหลาย agents ทำงานใน repo เดียวกัน

### 14.3 Four Workflow Modes

**Key message:** เลือก Sync, Async, Parallel หรือ Resync ตาม dependency และ ambiguity ของงาน

**Speaker script:** Sync ใช้เมื่องาน ambiguous ต้อง align ก่อน เช่น sprint planning หรือ architecture decision Async ใช้เมื่องานชัดและทำเสร็จแล้วค่อย review ได้ Parallel ใช้เมื่องาน independent จริง เช่น docs, tests และ implementation คนละ boundary Resync ใช้หลัง parallel work เพื่อ consolidate findings และ resolve conflicts ประโยคสำคัญคือถ้า output ของ A เป็น input ของ B งานนั้นไม่ใช่ parallel ต้อง sequence

### 14.4 Parallel Wave to Resync Sequence

**Key message:** Multi-agent workflow ควร fan-out เพื่อ analysis แล้ว resync เพื่อ human decision ก่อน implementation

**Speaker script:** Phase 1 Human Lead define problem แล้ว fan-out ไป PM Agent, Architect, Developer, Tester และ DevOps ให้ทำ analysis เฉพาะด้าน Phase 2 คือ Resync step ที่ synthesize, identify conflicts และ propose plan Phase 3 Human Lead review และ approve ก่อน implementation หลักคือให้ agents ช่วยขยายมุมมอง แต่ decision point ยังต้องรวมกลับมาที่ human

### 14.5 Coordination Rules vs Pitfalls

**Key message:** Same-repo coordination ต้องมีกฎ เช่น one owner per file, separate analysis from edits และ use branches for risky work

**Speaker script:** กฎ coordination มีไว้กัน pitfall ที่เกิดซ้ำครับ ถ้าไม่มี one owner per file จะเกิด merge conflicts ถ้า analysis กับ edits ทำพร้อมกันโดยไม่ align จะเกิด rework ถ้าไม่ใช้ branches สำหรับ risky work จะ contaminate main branch กฎเหล่านี้ไม่ได้ทำให้ช้าลง แต่ทำให้ parallel work reliable ขึ้น เพราะทุก agent รู้ boundary และขั้นตอนของตัวเอง

## Chapter 15

### 15.1 Eight-Agent Team Roster

**Key message:** Agent team แบ่งงานตาม SDLC phase เช่น Scout, Planner, Builder, Reviewer, Tester, Release และ Memory โดยมี Orchestrator คุม flow

**Speaker script:** ใน model นี้ Orchestrator delegate งานให้ specialist agents ตาม phase ครับ Scout ทำ context research, Planner ทำ wave plan และ task breakdown, Builder ทำ implementation diff และ PR, Reviewer ทำ review report, Tester ทำ validation results, Release ดู deploy status และ Memory บันทึก context ถาวร การแยก owner แบบนี้ลด role ambiguity และทำให้ handoff ชัดกว่าให้ agent ตัวเดียวทำทุกอย่าง

### 15.2 Agent Team vs Role-Based Subagents

**Key message:** Agent Team แบ่งตาม workflow stage และใช้ shared Team State เพื่อลด human dispatch bottleneck

**Speaker script:** Role-Based Subagents แบ่งตาม job title เช่น PM, Dev, QA และ human ต้องเรียกตาม role เอง ส่วน Agent Team Model แบ่งตาม workflow stage เช่น Scout ไป Build ไป Test โดย Orchestrator route ตาม completion scope ของแต่ละ agent คือ current stage และ context อยู่ใน shared Team State บวก Memory agent จุดเด่นคือ human ไม่ต้อง micro-dispatch ทุก transition

### 15.3 Nine-Step Agent Team Delivery Flow

**Key message:** Delivery flow ที่ดีมี human approval ที่ plan และ release พร้อม Memory Agent บันทึก handoffs ทุก step

**Speaker script:** Flow เริ่มจาก Feature Request ไป Scout research, Planner ทำ wave plan แล้วมี Human Approval จากนั้น Planner แตก task, Builder generate code, Reviewer review, Tester run test suite, Release package และมี Human Go/No-Go ก่อน deploy production Memory Agent เขียน context, handoffs, review logs และ test results ทุก step ทำให้ agent ถัดไปไม่ต้อง re-research และไม่พลาด decision สำคัญ

### 15.4 Agent Team Charter and Team State

**Key message:** Charter lock mission และ constraints ส่วน Team State track progress และ Handoff Packets ส่ง artifact ระหว่าง agents

**Speaker script:** Charter ระบุ mission, constraints, agents, success criteria และ handoff format เช่น adapter feature ต้องไม่มี direct DB writes และ tests ต้อง pass เมื่อเริ่มงาน Charter initialize Team State ที่บอก current_step, completed, pending และ last_handoff จากนั้น agent สร้าง Handoff Packet เช่น Builder ส่ง PR diff ไป Reviewer ข้อดีคือ context เดินทางผ่าน structure ไม่ใช่ข้อความ free-form ที่ตกหล่นง่าย

### 15.5 Guardrails and Pitfalls

**Key message:** Agent team ต้องมี guardrails เช่น charter, memory, handoff packets, human gates และ orchestrator routing เพื่อหลีกเลี่ยง scope drift และ silent errors

**Speaker script:** ฝั่ง guardrails เริ่มจาก Charter before agents start เพื่อกัน scope drift, Memory writes every step เพื่อกัน context loss, Handoff Packets เพื่อกันข้อมูลหาย, Human gates ที่ plan และ release เพื่อจับ bad plan หรือ broken release, และ Orchestrator routes work เพื่อไม่ให้ human micro-route ทุกอย่าง ฝั่ง pitfalls คือสิ่งตรงข้าม เช่น skipping charter, no memory, free-form handoffs หรือ zero gates ซึ่งทำให้ทีม AI เร็วแต่เสี่ยงมาก
