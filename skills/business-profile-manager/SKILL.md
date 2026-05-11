---
name: business-profile-manager
description: จัดการ business profile ของแต่ละเพจ (product/creator/personal_brand/hybrid) + style-notes feedback loop. Trigger เมื่อพูดถึง "เพิ่มเพจ", "ตั้งโปรไฟล์", "เพจสอน X", "เก็บ style", "ดู profile".
---

# Business Profile Manager

## Purpose

จัดการ business profiles ที่เป็น "บริบท" ให้ skill อื่นใน bsc-content-pipeline plugin (content-research, content-writer) อ่านไปใช้ ทำให้ระบบรองรับหลายเพจ/หลายธุรกิจ + หลาย business type

## Storage Location

ทุก profile เก็บที่ `business-profiles/<slug>/` ใน workspace folder ปัจจุบันของ Cowork session

```
business-profiles/
├── INDEX.md                       # auto-maintained list ของทุก profile
└── <slug>/
    ├── profile.yaml               # ข้อมูลหลัก
    ├── visual-style.yaml          # color, mood, สำหรับ image gen ภายหลัง
    └── style-notes.md             # ★ growth file — เพิ่มจาก feedback ทุกครั้ง
```

`<slug>` คือชื่อสั้นๆ kebab-case เช่น `cream-shop`, `ai-edu-thai`, `coach-john`

## Business Types

★ **อ่าน `references/business-types.md` ก่อนสร้าง/แก้ profile ทุกครั้ง**

plugin รองรับ 4 types — แต่ละ type ถามคำถามต่างกัน:
- `product` — ขายสินค้า/บริการ
- `creator` — content creator/educator (เพจสอน, เพจให้ความรู้)
- `personal_brand` — coach/consultant/expert
- `hybrid` — ผสม

## Operations

skill นี้รองรับ 5 operations หลัก ตัดสินใจจาก user request

### 1. List profiles

เมื่อผู้ใช้ถาม "มีเพจอะไรบ้าง", "list businesses", "ดู profiles"

อ่านไฟล์ทุกตัวใน `business-profiles/*/profile.yaml` แสดง table:

| Slug | Business Name | Type | Niche/Industry | Last Updated |

ถ้าไม่มี directory `business-profiles/` ให้สร้างก่อน แล้วบอก "ยังไม่มี profile — บอกผมว่าจะสร้างเพจไหน"

### 2. Create new profile (★ Type-aware)

เมื่อผู้ใช้บอก "เพิ่มเพจ X", "ตั้งโปรไฟล์ใหม่", "เพิ่มเพจ Content Creator"

**ขั้นตอน**:

#### Step A — Slug + Type
1. ถาม slug (ตรวจซ้ำ)
2. **ถาม business_type ก่อนเสมอ** ใช้ AskUserQuestion 4 options:
   - Product / Service business — เพจขายของ/บริการ
   - Content Creator / Educator — เพจสอน เพจให้ความรู้
   - Personal Brand / Professional — coach, consultant, expert
   - Hybrid — ผสม

   ถ้าผู้ใช้ไม่แน่ใจ — โชว์ decision tree จาก `references/business-types.md` แล้วถามใหม่

#### Step B — เก็บข้อมูลตาม type

**ถ้า type = `product`**: ใช้ flow 3 รอบเดิม
- รอบ 1 (Identity): business_name, niche/industry, products[], target_audience
- รอบ 2 (Voice): tone, perspective, do/don't
- รอบ 3 (Visual + CTA): สีหลัก, hashtag, CTA primary action+text

**ถ้า type = `creator`** ★ flow ใหม่:
- รอบ 1 (Identity creator):
  - business_name (ชื่อเพจ)
  - niche (★ บอกว่า narrow ดีกว่ากว้าง — ให้ตัวอย่าง)
  - **unique_perspective** (★ สำคัญมาก — มุมมองที่ทำให้คนติดตามคุณ ไม่ใช่เพจอื่น)
  - topics_covered[] (3-5 topics)
  - content_format_signature (รูปแบบ content เด่น)
- รอบ 2 (Audience):
  - persona_summary
  - questions_they_ask[] (3-5 คำถามที่กลุ่มเป้าหมายอยากรู้)
  - **audience_outcome** (★ หลังอ่านได้ insight อะไรกลับไป)
- รอบ 3 (Voice):
  - tone, perspective, formality, emoji
  - signature_phrases, banned_words
- รอบ 4 (Monetization + CTA):
  - monetization.models[] (ถ้ามี — ไม่บังคับ)
  - promo_frequency (★ default "1 ใน 5-10")
  - cta.primary_action (follow / save / share / comment)
  - cta.primary_text + secondary_text
  - links (course_page ถ้ามี)

**ถ้า type = `personal_brand`**:
- รอบ 1 (Identity professional):
  - business_name (ชื่อ + tagline สั้น)
  - professional_role
  - professional_journey (2-3 ประโยค)
  - credentials[]
  - unique_perspective
- รอบ 2 (Audience): เหมือน creator แต่เน้น client persona
- รอบ 3 (Voice): tone มักเป็น expert ไม่ใช่ peer
- รอบ 4 (CTA + Monetization):
  - cta.primary_action มักเป็น dm หรือ link ไป website
  - monetization (consulting / course / speaking)

**ถ้า type = `hybrid`**:
- ถามก่อน: components ที่ผสม (เลือก 2+ จาก product/creator/personal_brand)
- ถาม primary_component (ไหนคือ behavior หลัก)
- เก็บ field รวมจากทุก component แต่บอกผู้ใช้ว่ารอบจะเยอะหน่อย

#### Step C — Save
1. สร้าง `profile.yaml` จาก template + data ที่เก็บได้
2. สร้าง `visual-style.yaml` (visual fields ถามรอบ 4 หรือข้ามให้กรอกทีหลัง)
3. สร้าง `style-notes.md` ว่างพร้อม header
4. อัปเดต `business-profiles/INDEX.md`
5. แสดงสรุป + path

### 3. Show profile

เมื่อผู้ใช้บอก "ดู profile เพจ X"

อ่าน profile.yaml + style-notes.md แสดงเป็น human-readable summary แสดง:
- business_type ก่อนเสมอ (ระบุชัดว่าเพจไหนคือ type อะไร)
- field ตาม type — สำหรับ creator แสดง niche + unique_perspective + topics, ไม่แสดง products ว่าง
- จำนวน style notes
- monetization summary (ถ้ามี)

### 4. Edit profile

เมื่อผู้ใช้บอก "แก้ tone ของ <slug>", "เพิ่ม topic เพจ X"

1. โหลด profile ปัจจุบัน + รู้ business_type
2. AskUserQuestion เลือก field ตาม type ที่ relevant — ไม่โชว์ field ที่ไม่ใช้
3. แสดงค่าเก่า → ถามค่าใหม่
4. Edit YAML
5. ยืนยัน

**Type change**: ถ้าผู้ใช้อยากเปลี่ยน business_type (เช่น product → hybrid) — เตือนว่าต้อง add field ใหม่ของ type ที่เพิ่ม แล้วเดิน flow เก็บ field ใหม่

### 5. Append to style-notes (feedback loop)

★ **operation สำคัญที่สุด**

เมื่อผู้ใช้บอก "บันทึก feedback นี้", "เก็บการแก้นี้เป็น style"

1. หา slug (ถ้าไม่ระบุ ถาม)
2. รับข้อมูลใน 2 รูปแบบ:
   - **Rewrite**: before/after pair
   - **Rule**: instruction ตรงๆ
3. Append เข้า style-notes.md format:

```markdown
## YYYY-MM-DD - <Rewrite/Rule>

**Context**: <ทำไมเก็บ note นี้>

**Rule**: <statement สั้นๆ ที่ generalize ได้>

**Before** (ถ้ามี):
> <ข้อความก่อนแก้>

**After**:
> <ข้อความที่ผู้ใช้ต้องการ>

**Rationale**: <เหตุผล>

---
```

4. Confirm ก่อน save
5. หลัง save บอก path + จำนวน notes ทั้งหมด

content-writer จะอ่าน style-notes ทุกครั้งที่เขียน

## Active Profile Tracking

ระหว่าง session — จำ slug ที่ผู้ใช้ระบุครั้งแรก เป็น active profile

ถ้าผู้ใช้พูดคลุมเครือ — confirm: "ใช้เพจ <slug> ใช่ไหม?"

ถ้ายังไม่มี active + ไม่ระบุ — AskUserQuestion เลือกจาก list

## Validation Rules

- **slug**: lowercase, kebab-case, 3-30 ตัวอักษร
- **business_name**: ไม่ว่าง
- **business_type**: ต้องเป็น 1 ใน 4 ค่าที่ valid
- **type=product**: products[] ต้องมีอย่างน้อย 1 รายการ + แต่ละตัวมี target_pain
- **type=creator**: niche + unique_perspective + audience_outcome ต้องไม่ว่าง
- **type=personal_brand**: professional_role + professional_journey + unique_perspective ต้องไม่ว่าง
- **type=hybrid**: hybrid_components[] ≥ 2 + primary_component ต้องอยู่ใน components
- **CTA**: primary_action + primary_text ไม่ว่าง

ถ้า validation fail — AskUserQuestion เพื่อแก้ ไม่ save จนกว่าจะถูก

## Migration (จาก v0.1)

ถ้าโหลด profile ที่ไม่มี `business_type` field — แจ้งผู้ใช้:
> "Profile นี้ยังไม่ระบุ business_type (เพิ่มใน v0.2) อยากระบุตอนนี้ไหม?"

ถ้าระบุ — เดิน Step B ของ Create เพื่อเก็บ field ที่ขาด ไม่ทับ field ที่มี

## Output Format

ทุก operation จบด้วย:
- **What changed**: ไฟล์ไหน create/update
- **Where**: relative path จาก workspace
- **Next step**: เช่น "พร้อมรัน content-research แล้ว"

ใช้ภาษาไทย, technical terms (slug, YAML, type) คงอังกฤษ

## See Also

- `references/business-types.md` ★ — type definitions + decision tree
- `references/profile-fields.md` — คำอธิบายแต่ละ field
- `references/style-notes-examples.md` — ตัวอย่าง style notes
- `templates/profile.yaml`, `templates/visual-style.yaml`, `templates/style-notes.md`
