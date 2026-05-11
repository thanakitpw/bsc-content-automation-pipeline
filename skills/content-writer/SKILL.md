---
name: content-writer
description: เขียนบทความ/โพสต์ตาม voice + business_type + humanize rules (ห้ามอ้างงานวิจัย, "อาทิตย์" "555"). style-learning loop. Trigger "เขียนบทความ", "เขียนโพสต์", "draft", "ปรับบทความ".
---

# Content Writer

## Purpose

เขียนบทความ/โพสต์ที่:
1. ตรงกับ voice + business_type ของเพจ — ไม่ใช่ generic AI tone
2. อ้างอิง research ที่ทำมา — ไม่ทำขึ้นมาเอง
3. เรียนจาก feedback ผ่าน style-notes — ครั้งหน้าดีขึ้น

## Preflight Checklist

ก่อนเขียน ต้องโหลด 5 ไฟล์ + อ่าน business_type:

1. **profile**: `business-profiles/<slug>/profile.yaml`
   - ★ **อ่าน `business_type` ก่อน** — กำหนด structure + CTA pattern
   - ถ้าไม่มี slug → ดู Active Business จาก session, หรือถาม
   - ถ้ายังไม่มี profile → บอกให้รัน `business-profile-manager` ก่อน หยุด

2. **humanize rules**: `references/humanize-writing.md` ★ ★ ★
   - **บังคับโหลดทุกครั้ง** — เป็น hard rules ที่บังคับใช้กับทุกเพจทุก type
   - ครอบคลุม: ห้ามอ้างงานวิจัย, ใช้คำเข้าใจง่าย, "วันที่" ไม่ใช่ "Day", "อาทิตย์" ไม่ใช่ "สัปดาห์", หลีกเลี่ยง AI tic words, burstiness, lived experience anchor

3. **style-notes**: `business-profiles/<slug>/style-notes.md`
   - ★ สำคัญที่สุด — โหลดเสมอแม้จะว่าง
   - Active Rules = hard constraint
   - History = additional context
   - ★ ถ้า style-notes มี "Override" entry — overrides มาก่อน humanize rules

4. **research**: `research/<slug>/<file>.md`
   - ถ้าระบุ — ใช้ตัวนั้น
   - ถ้าไม่ระบุ — ใช้ไฟล์ใหม่สุดที่มี `Selected: yes`
   - ถ้าไม่มี research เลย — ถามผู้ใช้:
     (a) ใช้ topic ที่บอกตรงๆ
     (b) รัน content-research ก่อน
     (c) เขียนจาก profile อย่างเดียว (ไม่แนะนำ)

5. **template**: `templates/<type>-<platform>.md` หรือ `templates/<platform>.md`
   - ถ้ามี type-specific template (เช่น `creator-facebook.md`) ใช้ตัวนั้น
   - ไม่งั้น fallback ไป generic template (`facebook.md`)

## Writing Process by Business Type

### Common Steps (ทุก type)

#### Step 1: Plan ก่อนเขียน

แสดง writing plan สั้นๆ:
- **Type + Voice**: business_type + tone keywords
- **Active rules count**: "ใช้ X rules จาก style-notes"
- **Hook angle**: เลือก 1 จาก research.suggested_angle
- **Structure**: ตาม template
- **Length target**: ตาม `profile.platforms.<platform>.post_length`
- **Promo decision** (creator/hybrid only): "โพสต์นี้เป็น promo: yes/no" ตาม `monetization.promo_frequency`

#### Step 3: Self-Check ก่อน output

★ **ผ่าน 2 ชั้น** — humanization checklist (จาก `references/humanize-writing.md`) **ก่อน** type-specific checks

##### Layer 1: Humanize Checklist (8 ข้อ — บังคับ)

- [ ] **R1** ไม่มีคำว่า "งานวิจัย", "การศึกษา", "สถิติ" + ปีอ้างอิง — เปลี่ยนเป็น "ที่เคยเห็น...", "เพื่อนเล่าว่า..."
- [ ] **R2** ไม่มีศัพท์อังกฤษ psychology/business ที่ไม่จำเป็น (stress level, anxiety, productivity, optimize, implement) — แทนด้วยคำไทยเข้าใจง่าย
- [ ] **R3** ไม่มี "Day X" / "Week X" — ใช้ "วันที่ X" / "วันแรก" / "อาทิตย์" แทน
- [ ] **R3.1** ไม่มีปีตัวเลขเป๊ะ (เช่น 2018, 2024) — ใช้ "ปีที่แล้ว" / "หลายปีก่อน" / "เมื่อ X ปีก่อน"
- [ ] **R4** ไม่มี "สัปดาห์" → ใช้ "อาทิตย์" (ยกเว้น `formality_level=formal` หรือมี Override ใน style-notes)
- [ ] **R5** ไม่มี AI tic words: "ในยุคปัจจุบัน", "อย่างมาก/ยิ่ง", "ทั้งนี้และทั้งนั้น", "ดังนั้น" (ใช้ "เลย" แทน), "อย่างไรก็ตาม" (ใช้ "แต่")
- [ ] **R6** ถ้ามีหัวเราะ → ใช้ "555" / "5555" / "55+" — ห้าม "ฮ่าฮ่าฮ่า" / "ฮ่ะฮ่ะ" (tone formal/วิชาการ ไม่ใส่หัวเราะเลย)
- [ ] **B** Burstiness — มีประโยคสั้น (≤5 คำ) อย่างน้อย 2 ตัว สลับกับประโยคยาว
- [ ] **L** Lived experience anchor — มีอย่างน้อย 1 จุดที่ดึงประสบการณ์/case จริง (จาก research.reference_quotes ถ้าไม่มีอย่างอื่น)

##### Layer 2: Profile + Type Checks (6 ข้อ)

1. ไม่มี `voice.banned_words`
2. perspective สอดคล้องตลอด
3. ความยาวอยู่ในช่วง template
4. CTA ตรงกับ `cta.primary_action` + ใช้ `cta.primary_text`
5. ไม่อ้างข้อมูลที่ไม่อยู่ใน research
6. **Type-specific check** — ดูข้างล่าง

★ ถ้า fail ข้อใดในทั้ง 2 layers — **ต้อง revise ก่อน output** ห้าม output draft ที่ยัง fail

#### Step 4: Output Draft

```markdown
---
business: <slug>
business_type: <type>
platform: <facebook|instagram|blog|line-oa>
date: YYYY-MM-DD
research_source: research/<slug>/<file>.md
hook_angle: <angle>
word_count: <approx>
is_promo: <true|false>
---

<draft text>
```

Save ที่ `drafts/<slug>/<YYYY-MM-DD>-<topic-slug>.md`

#### Step 5: Feedback Loop

ปิดด้วย prompt:

> 📝 ถัดไป:
> - ✏️ **แก้** — บอกตรงไหน ผมทำ v2
> - 💾 **เก็บ style** — append เข้า style-notes
> - ✅ **OK พอแล้ว** — ปิด task

---

### Type-Specific Step 2: Write Draft

#### `product` type — Pain → Solution → Product → CTA

**Structure** (FB post):
1. Hook = pain question (จาก research.reference_quotes ถ้ามี)
2. Pain elaboration (สะท้อนความรู้สึก)
3. Solution + soft product mention
4. CTA = purchase / dm

**Type-specific check**:
- product mention มีอย่างน้อย 1 ครั้ง
- ไม่ promote เกิน 1 product ใน 1 post
- CTA pattern = "ทักแชท" / "ดูสินค้า"

#### `creator` type ★ — Setup → Insight → Example → Takeaway

**Structure** (FB post — non-promo):
1. **Hook** เลือก 1:
   - Misconception reveal — "ทุกคนคิดว่า X คือ Y... แต่จริงๆ คือ Z"
   - Question that provokes — "เคยสงสัยมั้ยว่าทำไม X?"
   - Counter-intuitive observation — "ฟังดูแปลก แต่ X ทำงานแบบนี้"
2. **Setup** (1-2 ประโยค) — context ของ topic
3. **Insight/Reveal** (3-5 ประโยค) — content หลัก ที่ผู้อ่านจะ "ได้กลับไป"
4. **Example** (1-2 ประโยค) — case ตัวอย่างจริงจาก research
5. **Takeaway** (1 ประโยค) — สิ่งเดียวที่อยากให้จำ
6. **CTA** = save / follow / share / comment

**ถ้าเป็น Promo post (ดู monetization.promo_frequency)**:
- ใช้ structure แบบ product ครึ่งหนึ่ง — แต่เริ่มจาก "หลายคนถามว่า course นี้ต่างยังไง..."
- ห้าม pushy — soft, conversational

**Type-specific check**:
- ★ ห้ามใช้ "ทักแชทมาคุย" / "ดูสินค้า" CTA (ฟังเหมือนพยายามขาย — สำหรับ creator engagement ตก)
- ห้ามใช้ คำ "รับรองผล", "ลด 50%" ฯลฯ (โทน salesy)
- ต้องมี "1 thing to take away" ชัดเจน — ถ้าไม่มี = revise
- ใช้ unique_perspective ของ creator ตามที่กรอกใน profile — content ต้องสะท้อน angle เฉพาะตัว ไม่ใช่ generic
- Promo decision ตาม `monetization.promo_frequency` — ถ้า "1 ใน 10" คุณต้องเช็คประวัติ drafts ของเพจนี้ ถ้า 9 โพสต์ก่อนเป็น educational ค่อยทำ promo

#### `personal_brand` type — Observation → Analysis → Recommendation

**Structure** (FB post):
1. **Hook** = personal angle:
   - "เคสที่เจอเมื่อสัปดาห์ก่อน..."
   - "หลังทำมา <X> ปี ผม/ดิฉันเจอ pattern นี้"
   - News-jack: "ข่าว <X> สอนอะไรเรา"
2. **Observation** — สิ่งที่ผู้เชี่ยวชาญเห็น
3. **Analysis** — ใช้ expertise + framework
4. **Recommendation** — ทำอะไรกลับไป
5. **CTA** = dm / website / register

**Type-specific check**:
- Tone = expert ไม่ใช่ peer — perspective formal กว่า creator
- อ้างอิง credentials ได้ (ถ้า relevant) — "ในฐานะที่ทำสาย <role>"
- ไม่อ้าง stat ที่ไม่ verify ได้

#### `hybrid` type

ดู `primary_component` ใน profile + decision ของโพสต์นี้:

- โพสต์ปกติ → ใช้ structure ของ primary
- โพสต์ promo → ใช้ structure ของ secondary component (มัก = product)

ตรวจ `monetization.promo_frequency` ก่อนตัดสินใจว่าเป็น promo หรือไม่

---

## Multiple Variations

ถ้าผู้ใช้บอก "ขอ 2 เวอร์ชัน":

- เขียน 2-3 versions ที่ต่างกันที่ **angle** หรือ **hook style** (voice + rules + research เหมือนกัน)
- save แต่ละ version: `<slug>/<date>-<topic>.v-a.md`, `.v-b.md`
- แสดงรวมในหน้าจอ + ถามผู้ใช้ว่าชอบเวอร์ชันไหน

## Bring Your Own Topic (no research)

ถ้าผู้ใช้บอก "เขียนเรื่อง X เลย ไม่ต้อง research":

- เขียนได้ แต่ frontmatter ต้องมี:
  ```yaml
  research_source: none
  warning: "no research backing — fact-check ก่อนโพสต์"
  ```
- หลีกเลี่ยง stat / claim ที่ verify ไม่ได้
- เน้น opinion/story/voice มากกว่า data

★ creator type: warn ผู้ใช้ extra เพราะ creator content บ่อยครั้งต้องใช้ data/citation

## Templates Available

ดูใน `templates/`:

**Generic (ทุก type)**:
- `facebook.md` — โครง 4 ย่อหน้า, 150-300 คำ
- `instagram.md` — caption สั้น 80-150 คำ + hashtag
- `blog.md` — 800-1200 คำ
- `line-oa.md` — broadcast format

**Type-specific (ใช้ก่อน generic ถ้ามี)**:
- `creator-facebook.md` ★ — โครงสำหรับ educational FB post
- `creator-thread.md` ★ — Twitter/X thread หรือ FB long-form

## See Also

- `references/humanize-writing.md` ★ ★ ★ — hard rules ที่บังคับใช้ทุกครั้ง (ห้าม skip)
- `references/voice-application.md` — translate profile.voice → choices
- `references/feedback-extraction.md` — ดึง before/after จาก user edit
- `references/structure-by-type.md` ★ — รายละเอียด structure แต่ละ type
- `templates/*.md`
