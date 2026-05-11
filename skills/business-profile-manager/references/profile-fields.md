# Profile Fields Reference

คำอธิบายแต่ละ field ของ `profile.yaml`

★ ดู `business-types.md` ก่อน — type ของเพจกำหนดว่า field ไหนต้องกรอก

## Core Fields (ทุก type)

### slug
- ✅ `cream-nicha`, `ai-edu-thai`, `coach-john`
- ❌ `ครีมNicha` (ไทย), `Cream Shop` (เว้นวรรค), `c` (สั้นไป)

### business_name
ชื่อแบรนด์/เพจที่ผู้ใช้จะเอาไปใช้ติดต่อจริง — ตรงกับชื่อบนหน้าเพจ

### business_type
1 ใน 4 ค่า: `product` | `creator` | `personal_brand` | `hybrid`
ดู `business-types.md` สำหรับ definition + decision tree

---

## Identity Fields by Type

### Common (ทุก type)

#### identity.niche
scope แคบของเพจ — ★ creator: narrow ดีกว่ากว้าง

ดี:
- `"AI สำหรับ marketer ไทย"` (creator)
- `"ครีมสิวฮอร์โมนสำหรับวัย 30+"` (product)
- `"Brand strategist สำหรับ SME ไทย"` (personal_brand)

ไม่ดี:
- `"AI"` (กว้างเกิน — แข่งกับเพจ AI ใหญ่ๆ ไม่ได้)
- `"ครีม"` (กว้างเกิน)

#### identity.unique_perspective
★ สำคัญที่สุดสำหรับ creator/personal_brand

มุมมอง/angle ที่ทำให้คนติดตามคุณ ไม่ใช่เพจอื่นในวงการเดียวกัน

ดี:
- `"ใช้กรณีศึกษาจริงทุกครั้ง — ไม่พูดทฤษฎีลอยๆ"`
- `"เน้นเชื่อมต่อกับวัฒนธรรมไทยและบริบทท้องถิ่น"`
- `"อธิบายเรื่องยากให้คนไม่ใช่สาย tech เข้าใจ"`

ไม่ดี:
- `"พยายามทำให้ดี"` (กว้างไป)
- `"ความรู้ลึก"` (ใครก็พูดได้)

---

### Product Type

#### identity.products[]
แต่ละสินค้าควรมี: name, description, price_range, target_pain

ตัวอย่างที่ดี:
```yaml
products:
  - name: "ครีมลดสิว Acne Clear"
    description: "ครีมเฉพาะจุดสำหรับสิวอักเสบ ใช้ก่อนนอน"
    price_range: "590-790 บาท"
    target_pain: "สิวอักเสบเรื้อรังที่ยาในร้านขายยาไม่หาย"
```

ตัวอย่างที่ไม่ดี (กว้างเกิน):
```yaml
products:
  - name: "ครีม"
    description: "ครีมดี"
    target_pain: "หน้าไม่สวย"
```

---

### Creator Type ★

#### identity.topics_covered[]
หัวข้อหลักที่เพจครอบคลุม 3-5 ตัว

ตัวอย่างที่ดี (เพจ "AI สำหรับ marketer"):
```yaml
topics_covered:
  - "พื้นฐาน AI ที่ marketer ต้องรู้ใน 2026"
  - "Use case AI ในงาน digital marketing"
  - "เครื่องมือ AI ที่ใช้งานจริงในไทย"
  - "ผลกระทบ AI กับอาชีพ marketing"
```

ตัวอย่างที่ไม่ดี:
- `["AI"]` (กว้างเกิน)
- `["เรื่องใน AI 100 เรื่อง"]` (ครอบคลุมเกิน — ไม่มี focus)

#### identity.expertise_areas[]
ทักษะ/ความรู้ที่ creator มี ใช้บ่งบอกว่าเขียนเรื่องไหนได้น่าเชื่อถือ

#### identity.content_format_signature
รูปแบบ content เด่นที่เพจเลือกใช้สม่ำเสมอ

ตัวอย่าง:
- `"Thread ยาว 8-12 ทวีต พร้อม diagram 1 ภาพ"`
- `"Infographic + caption สั้น 50-100 คำ"`
- `"Deep-dive blog 1500 คำ + summary FB"`
- `"Carousel 7 slides — 1 idea per slide"`

#### target_audience.questions_they_ask[]
★ แทน pain_points ของ product type

คำถามที่กลุ่มเป้าหมายค้นหา/อยากรู้ — เป็น input หลักของ content-research

ตัวอย่างที่ดี (เพจ AI สำหรับ marketer):
```yaml
questions_they_ask:
  - "AI จะเข้ามาแทนงาน marketer ไหม"
  - "เริ่มเรียน AI ตรงไหนดี ถ้าไม่ใช่สาย tech"
  - "เครื่องมือ AI ตัวไหน free แล้วใช้งานจริงได้"
  - "วิธีเขียน prompt ให้ AI ทำงาน marketing"
```

#### target_audience.audience_outcome
หลังอ่านโพสต์เดียวจะได้อะไรกลับไป

ตัวอย่าง:
- `"เข้าใจ concept AI 1 ตัวที่ใช้งานได้จริงในวันรุ่งขึ้น"`
- `"รู้ว่า trend นี้กระทบงานตัวเองยังไง"`

---

### Personal Brand Type

#### identity.professional_role
title + scale/ปี — บอกว่าเป็นใคร

ตัวอย่าง:
- `"Brand Strategist 12 ปี — ทำงานกับ SME 80+ บริษัท"`
- `"หมอผิวหนังคลินิก ABC 8 ปี เน้นรักษาสิวฮอร์โมน"`

#### identity.professional_journey
2-3 ประโยค journey สั้น ใช้ใน bio + intro post

#### identity.credentials[]
ปริญญา/cert/ประสบการณ์ที่อ้างอิงได้

---

## Voice Fields (ทุก type)

### voice.tone
preset แนะนำ:
- `กันเอง` — เพื่อน, ใช้ "เรา"
- `ทางการ` — สุภาพ, "ดิฉัน"
- `ขายของ` — energetic (ใช้กับ product)
- `วิชาการ` — มีอ้างอิง (ใช้กับ creator/personal_brand)
- `expert` — authority tone (ใช้กับ personal_brand)

custom ได้ — เก็บคำอธิบายตรงๆ

### voice.do / dont
bullet สั้น ทำตามได้จริง

ตัวอย่างดี (creator):
- ✅ "เปิดด้วย misconception ที่คนเข้าใจผิด"
- ✅ "ห้าม claim ว่ารู้ทุกอย่าง — ยอมรับ uncertainty"

### voice.signature_phrases
คำที่อยากให้ปรากฏซ้ำเพื่อ brand recall

### voice.banned_words
content-writer จะเช็คก่อน output — exact match search

---

## Audience Fields

### persona_summary (ทุก type)
1-2 ประโยคบอกใครคือลูกค้า/ผู้ติดตามในอุดมคติ

### audience_outcome (ทุก type) ★
ผู้ติดตาม/ลูกค้าได้อะไร — ต่างกันตาม type:
- product: "แก้ pain X ด้วยสินค้า"
- creator: "เข้าใจ <topic> แบบลึกขึ้น"
- personal_brand: "เข้าถึง insight ระดับมืออาชีพ"

---

## Monetization (optional)

### monetization.models[]
ระบุ revenue stream ทั้งหมด — `[]` ถ้าไม่ commercialize:
- `direct_sales` — product type ใช้
- `course` — creator/personal_brand
- `affiliate` — creator
- `sponsorship` — creator
- `consulting` — personal_brand
- `ad_revenue` — creator
- `patreon` — creator
- `none` — ไม่มี

### monetization.promo_frequency
- `"ทุกโพสต์"` — product type
- `"1 ใน 5"` — creator แบบ commercialize
- `"1 ใน 10"` — creator pure educational
- `"ตอนเปิดรับ"` — personal_brand consulting

★ creator: เกิน 1 ใน 5 โดยทั่วไป engagement ตก

---

## CTA Pattern (ต่างกันตาม type)

### cta.primary_action
- `purchase` — product
- `dm` — product/personal_brand
- `follow` — creator
- `save` — creator (educational content)
- `share` — creator
- `comment` — creator (engagement bait)
- `subscribe` — creator (newsletter/youtube)
- `register` — creator/personal_brand (course/event)

### cta.primary_text
ข้อความ CTA หลัก — ตัวอย่างตาม type:

**Product**:
- "ทักแชทมาคุยฟรี"
- "ดูสินค้าเพิ่มที่ลิงก์ใต้คอมเมนต์"

**Creator**:
- "Save ไว้อ่านทีหลัง"
- "Follow เพื่อเรื่องต่อไปในหัวข้อนี้"
- "Comment ว่าอยากให้เล่าเรื่องไหนต่อ"
- "Share ให้เพื่อนที่ต้องอ่านบ้าง"

**Personal Brand**:
- "DM มาปรึกษาเคสคุณได้"
- "ดูบริการที่ website"

---

## Content Pillars (default ตาม type)

| Type | Pillar 1 | Pillar 2 | Pillar 3 | Pillar 4 |
|------|----------|----------|----------|----------|
| product | Education 50% | Soft Sell 30% | Promo 20% | — |
| creator | Education 70% | Story 20% | Promo 10% | — |
| personal_brand | Insight 40% | Story/Case 30% | Industry commentary 20% | Promo 10% |

ปรับสัดส่วนตาม goal ของเพจได้

---

## Style Anchors

ตัวอย่างบทความเก่าที่ชอบ — content-writer อ่านเป็น reference

แนะนำให้มี 3-5 บทความหลากประเภท

ใส่ได้ 2 รูปแบบ:
1. **Path**: `drafts/2026-01-15-วิธีล้างหน้าถูกต้อง.md`
2. **Inline**: paste ตรงๆ ใน YAML (`|` block scalar)

```yaml
style_anchors:
  - path: "drafts/2026-01-15-วิธีล้างหน้าถูกต้อง.md"
  - inline: |
      หลายคนล้างหน้าผิดวิธีโดยไม่รู้ตัว
      ทีมเราเลยมาเล่าให้ฟัง 3 ขั้นตอน...
```
