---
name: content-planner
description: วาง content plan รายเดือนต่อเพจ — pillar ratio + slots + backlog + breaking handling (add ไม่ swap). Trigger "วาง plan", "plan เดือนนี้", "ดู calendar", "เพิ่ม breaking", "view plan".
---

# Content Planner

## Purpose

จัดการ content calendar รายเดือนของแต่ละเพจ — รวมการวาง pillar ratio, schedule slot, จัดการ backlog (stock ของ topic ที่ research แล้ว), และรับมือ breaking content (add slot ใหม่ในวันเดียวกัน ไม่ swap ของเดิม)

## Storage

```
plans/<slug>/<YYYY-MM>.yaml          # 1 ไฟล์ต่อเดือนต่อเพจ
```

## State File Schema

```yaml
month: "2026-05"
target_count: 12                  # โพสต์ทั้งเดือน
posting_frequency: "3/week"       # human-readable

pillar_ratio:                      # target reference
  Education: 0.70
  Story: 0.20
  Promo: 0.10

backlog:                           # stock ของ topic ที่ research แล้ว
  - id: bl-001
    research_file: research/<slug>/<date>-<topic>.md
    topic_title: "AI agent ≠ ChatGPT"
    pillar: Education
    priority: high                 # high / medium / low
    added_at: "2026-04-28"

slots:                             # โพสต์ที่ schedule
  - id: 1
    date: 2026-05-02
    pillar: Education
    topic: "AI agent ≠ ChatGPT"
    status: posted                 # planned / drafted / final / posted / missed
    research_file: research/<slug>/<file>.md
    draft_path: drafts/<slug>/<file>.md
    final_path: final/<slug>/<N>-<topic>/
    posted_at: "2026-05-02"

  - id: 2
    date: 2026-05-04
    pillar: Education
    topic: "เคสลูกค้าใช้ AI ผิดทาง"
    status: planned

  # Breaking — date เดียวกับ id:2 (2 โพสต์/วัน)
  - id: 3
    date: 2026-05-04
    pillar: Education
    topic: "OpenAI GPT-5 — marketer ต้องรู้อะไร"
    status: planned
    is_breaking: true
    triggered_by: "OpenAI announcement 2026-05-04"
```

## Operations

skill มี 6 operations:

### 1. `plan-month` — สร้าง/edit plan ของเดือน

เมื่อผู้ใช้บอก "วาง plan เดือน X", "plan เดือนนี้"

ขั้นตอน:
1. ดูว่า `plans/<slug>/<YYYY-MM>.yaml` มีอยู่แล้วไหม
   - **มี** → ถาม "edit หรือ overwrite"
   - **ไม่มี** → สร้างใหม่
2. ถาม + เก็บค่า:
   - `target_count` (default: 12)
   - `posting_frequency` (default: "3/week")
   - `pillar_ratio` (default: จาก `profile.content_pillars` ของเพจนั้น)
3. สร้าง slots placeholder ตาม posting_frequency (e.g. ทุก Mon/Wed/Fri ของเดือน) status = `open`
4. แสดง summary + path

### 2. `plan-week` — assign topic ลง slot

เมื่อผู้ใช้บอก "plan อาทิตย์นี้", "assign topic อาทิตย์ที่ N"

ขั้นตอน:
1. โหลด plan ของเดือนปัจจุบัน
2. หา slots ในอาทิตย์ที่ระบุ ที่ status=`open`
3. โหลด `backlog[]` ที่ priority สูงสุด + ตรง pillar ที่ slot ต้องการ
4. สำหรับแต่ละ open slot — AskUserQuestion เลือก topic จาก backlog (หรือ "skip / open ไว้ก่อน")
5. เลือกแล้ว → ย้ายจาก `backlog[]` → `slots[].topic` + status = `planned`
6. ถ้า backlog ว่างเปล่า / topic ไม่พอ → แจ้ง "backlog ขาด — รัน content-research เพิ่ม"

### 3. `add-breaking` ★ — เพิ่ม breaking content

เมื่อผู้ใช้บอก "เพิ่ม breaking", "มี post ด่วน", "breaking content"

ขั้นตอน:
1. ถาม:
   - **topic**: เรื่องที่จะโพสต์
   - **date**: default = วันนี้
   - **pillar**: default = ใช้ pillar เดียวกับ slot ที่มีในวันนั้น (ถ้ามี) / ถ้าไม่ → ถาม
   - **triggered_by**: เหตุการณ์/ข่าวที่ trigger
2. ★ **Append** เป็น slot ใหม่ — ไม่ swap, ไม่กระทบ slot เดิม
3. mark `is_breaking: true` + `triggered_by: "..."`
4. status = `planned`
5. แสดงสรุป + **ไม่ auto-trigger** research/writer — บอกผู้ใช้ว่า:
   > "Breaking slot เพิ่มแล้ว (id:N, date:Y)
   > ต่อไป รัน content-research แล้ว content-writer ตามขั้นตอน"

### 4. `view-calendar` — แสดง overview

เมื่อผู้ใช้บอก "ดู calendar", "view plan", "เดือนนี้มีอะไรบ้าง"

★ แสดง **เฉพาะเดือนปัจจุบัน** (ไม่ load เดือนอื่น)

Format:

```
🗓 May 2026 — <slug>
─────────────────────────────────
Mon 2026-05-02  🟢 [Edu]  AI agent ≠ ChatGPT
Wed 2026-05-04  🔵 [Edu]  เคสลูกค้าใช้ AI ผิดทาง
                🔴 [Edu]  OpenAI GPT-5 (breaking)
Fri 2026-05-07  🟡 [Story] เคสลูกค้าใช้ AI ผิด
Mon 2026-05-09  ⚪ [open]
...

─────────────────────────────────
📊 Stats:
   Posts this month: 4/12
   Pillar ratio actual: Edu 75% | Story 25% | Promo 0%
   target: Edu 70% / Story 20% / Promo 10%
   ℹ️ Promo ขาด — schedule ก่อนสิ้นเดือน

📂 Backlog: 2 topics
   - [high] [Edu] AI search disruption
   - [med]  [Edu] Prompt vs Context engineering

Status legend:
   🟢 posted   🟡 drafted   🔵 planned   ⚪ open   🔴 breaking
```

### 5. `health-check` — review สำหรับ weekly

เมื่อผู้ใช้บอก "health check", "review plan", "เช็คอะไรขาด"

แสดง info (ไม่ block, ไม่ warning):

- **Pillar ratio drift** — pillar ไหน actual ห่างจาก target เกิน 15%
- **Backlog low** — backlog < 3 รายการ → "ควรรัน content-research เพิ่ม"
- **Backlog expiry** — topic ใน backlog เกิน 60 วัน → "topic อาจ outdated, review หรือ remove"
- **Missed slots** — slot ในอดีตที่ยัง `open` หรือ `planned` (ไม่ได้โพสต์) → "วันที่ X — mark missed / skip / move ไปวันอื่น?"
- **Breaking ratio** — info เฉยๆ: "เดือนนี้ breaking N โพสต์ จาก M (X%)"

### 6. `sync-status` — อัปเดต status จากไฟล์จริง

เมื่อผู้ใช้บอก "sync", "update status", หรือเรียกอัตโนมัติก่อน view-calendar

logic:
- ถ้ามี `drafts/<slug>/<topic>.md` → status = `drafted`
- ถ้ามี `final/<slug>/<N>-<topic>/` → status = `final`
- status = `posted` ต้อง user mark เอง ("mark posted slot X")

## Backlog Management

### Add to backlog

ตอน content-research จบ + user เลือก topic 1 ตัวจาก 5-10:
- topic ที่เลือก → ใช้เขียน
- topic ที่เหลือ — content-research ถาม "เก็บใน backlog ไหม" → ถ้าใช่ append เข้า `backlog[]` ของ plan เดือนปัจจุบัน

หรือ user manual:
> "เพิ่ม topic '...' เข้า backlog"

### Remove from backlog

- เมื่อ topic จาก backlog ถูก assign ลง slot — auto remove
- User manual: "ลบ backlog id bl-XXX"
- Health-check เตือนถ้าเก่าเกิน 60 วัน — user decide remove หรือ keep

### Backlog priority

- `high` — เรื่องด่วน, trend ที่หมดอายุเร็ว
- `medium` — default
- `low` — evergreen, ใช้เป็น filler ตอน inspiration ตัน

## Active Plan Tracking

ระหว่าง session — จำเดือนที่ผู้ใช้ทำงานเป็น "active plan" ครั้งแรก เก็บไว้ใน working memory
ถ้าผู้ใช้พูด "ดู calendar" โดยไม่ระบุเดือน — ใช้ active plan

★ ถ้า active plan ไม่ตรงกับเดือนปัจจุบัน (system date) — แสดง warning + ถาม "switch ไปเดือนปัจจุบันไหม"

## Integration กับ skills อื่น

- **content-research** → output ของ research อาจ append เข้า backlog (ตามที่ user เลือก)
- **content-writer** → อ่าน slot ที่ user ระบุ → ดู research_file → เขียน → mark status `drafted`
- **post-formatter** → mark slot `final` + update `final_path`

content-planner ไม่ auto-trigger skill อื่น (★ user manual ทุกครั้ง — ตามที่ user request)

## Output Format

ทุก operation จบด้วย:
- **What changed**: slot/backlog ไหน update
- **Where**: path
- **Next step**: suggestion (เช่น "ต่อไป รัน content-research")

## Validation

- **target_count**: 1-50 ต่อเดือน
- **posting_frequency**: free text แต่ parse pattern X/week
- **pillar_ratio**: ทุก key รวม ≈ 1.0 (tolerance 0.05)
- **slot.date**: ภายในเดือนที่ระบุใน `month` field
- **slot.pillar**: ต้องอยู่ใน `pillar_ratio` keys หรือเป็น `flex`

## See Also

- `business-profiles/<slug>/profile.yaml` — `content_pillars` เป็น default ของ pillar_ratio
- `research/<slug>/` — research files ที่อ้างใน backlog/slots
- `drafts/<slug>/`, `final/<slug>/` — files ที่ sync-status ตรวจ
