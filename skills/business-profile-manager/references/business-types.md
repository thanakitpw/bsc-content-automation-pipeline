# Business Types

ทุก profile ใน plugin นี้ต้องระบุ `business_type` 1 ใน 4 ค่า เพราะมันเปลี่ยนวิธีถามคำถาม + วิธี research + วิธีเขียน

ทุก skill (`business-profile-manager`, `content-research`, `content-writer`) อ่านไฟล์นี้เป็น behavior reference

---

## 1. `product` — Product / Service Business

### นิยาม
ธุรกิจที่ขายสินค้าหรือบริการตรงๆ — รายได้หลักจาก transaction กับลูกค้า

### ตัวอย่าง
- เพจขายครีม / สกินแคร์ / อาหารเสริม
- ร้านอาหาร / คาเฟ่
- คลินิก / สปา / นวด
- บริการ home service (ทำความสะอาด, repair)
- e-commerce, fashion, gadget

### Required Fields (เพิ่มจาก core)
- `identity.products[]` — ต้องมีอย่างน้อย 1 รายการพร้อม `target_pain`
- `target_audience.primary.pain_points[]` — pain ที่สินค้าตอบโจทย์
- `cta.primary_action` — มักเป็น `purchase` / `dm`

### Default Behavior
- **Research**: Track 1 (web trend) + Track 2 (social listening pain) + Track 3 (competitor) — ครบทั้ง 3
- **Writer**: hook = pain question, structure = pain → solution → product → CTA
- **CTA pattern**: "ทักแชทมาคุย", "ดูสินค้าที่ลิงก์", "สั่งเลย"
- **Content pillars default**: Education 50%, Soft Sell 30%, Promo 20%

---

## 2. `creator` — Content Creator / Educator

### นิยาม
เพจที่ขาย "ความรู้ + attention + perspective" ไม่ใช่สินค้า รายได้ (ถ้ามี) มาจาก ad / sponsorship / affiliate / course / patreon

### ตัวอย่าง
- เพจสอน skill: "AI สำหรับ marketer", "Excel รอบตัว", "Coding for Beginners"
- เพจให้ความรู้สายวิชาการ: "ประวัติศาสตร์ไทย", "ฟิสิกส์ในชีวิตประจำวัน"
- เพจรีวิว/curation: "รีวิวร้านอาหาร", "Tech roundup"
- เพจ explainer: "เศรษฐกิจง่ายๆ", "กฎหมายสำหรับมนุษย์เงินเดือน"

### Required Fields (เพิ่มจาก core)
- `identity.niche` — narrow scope ★ สำคัญสุด
- `identity.unique_perspective` — ★ ต้องมี เพราะ creator แข่งกับเพจอื่นในวงการเดียวกัน
- `identity.topics_covered[]` — ครอบคลุมเรื่องอะไรบ้าง
- `target_audience.primary.questions_they_ask[]` — แทน pain_points
- `target_audience.audience_outcome` — ผู้ติดตามได้ insight อะไร
- `cta.primary_action` — มักเป็น `follow` / `save` / `share` / `comment`

### Optional Fields
- `monetization.models` — ถ้ามี course/affiliate/sponsorship ระบุได้
- `monetization.promo_frequency` — แนะนำ "1 ใน 5-10" ไม่บ่อย

### Default Behavior
- **Research**: Track 1 (web trend) + Track 2 (questions/misconceptions ใน niche) + Track 3 (creator คู่แข่ง — ดู gap)
  - ★ เพิ่ม: หา **misconceptions** ที่คนเข้าใจผิดในวงการ — เป็น hook ที่ creator ใช้ได้ดี
- **Writer**:
  - Hook = "ทุกคนเข้าใจผิดเรื่องนี้..." / "วันนี้มาเล่าเรื่อง <topic>" / question ที่ provoke
  - Structure = setup → reveal/insight → example → takeaway
  - **ไม่ใส่ promo ทุกโพสต์** — ทำตาม `monetization.promo_frequency`
- **CTA pattern**: "Save ไว้อ่าน", "Follow เพื่อเรื่องต่อไป", "Comment ว่าอยากให้เล่าเรื่องไหน", "Share ให้เพื่อนที่ต้องอ่าน"
- **Content pillars default**: Education 70%, Story/Case 20%, Promo 10%

### Anti-patterns สำหรับ Creator
- ❌ ใส่ "ทักแชทมาคุย" CTA — ฟังเหมือนพยายามขาย
- ❌ Promo ทุกโพสต์ — ทำให้ engagement ตก
- ❌ Topic กว้างไม่ใช่ niche — แข่งกับเพจใหญ่ไม่ได้

---

## 3. `personal_brand` — Personal Brand / Professional

### นิยาม
แบรนด์ส่วนตัวของผู้เชี่ยวชาญ — coach, consultant, freelancer, expert ที่ใช้ social เป็นช่องทาง position ตัวเอง รายได้มาจาก consulting / client work / speaking

### ตัวอย่าง
- Brand strategist ที่ post insight + รับ consulting
- หมอ/นักจิตวิทยาที่แชร์ความรู้ + รับเคส
- Freelance designer/dev ที่แชร์งาน + รับ project
- Author/speaker ที่ขายหนังสือ/talk

### Required Fields (เพิ่มจาก core)
- `identity.professional_role` — title + ปี/scale
- `identity.professional_journey` — เล่า journey 2-3 ประโยค
- `identity.unique_perspective` — มุมที่ทำให้แตกต่างจากคนสายเดียวกัน
- `target_audience.audience_outcome` — ผู้ติดตามได้อะไร
- `cta.primary_action` — มักเป็น `dm` / `follow` / link ไป website

### Default Behavior
- **Research**: Track 1 + 2 (focus pain ของ client ที่ผู้เชี่ยวชาญแก้) + Track 3 (เพื่อน-สายเดียวกัน)
- **Writer**:
  - Hook มักเปิดด้วย personal angle — "เคสที่เพิ่งเจอ", "หลังทำมา X ปี ผม/ดิฉันเจอว่า..."
  - Tone = expert ไม่ใช่ peer
  - Structure = observation → analysis → recommendation
- **CTA pattern**: "DM มาปรึกษา", "ดู website", "Follow เพื่อ insight ต่อไป"
- **Content pillars default**: Insight 40%, Story/Case 30%, Industry commentary 20%, Promo 10%

---

## 4. `hybrid` — Hybrid

### นิยาม
ผสม 2 type ขึ้นไป — มี audience แบบ creator แต่ขายของ/course/service ด้วย

### ตัวอย่าง
- Creator สอน Excel + ขาย course Excel
- Personal brand ที่ขาย service + content educational
- Influencer ที่ขายสินค้า affiliate + เนื้อหาให้ความรู้

### Required Fields
- รวมจาก type หลัก + type รอง — `business-profile-manager` ถามทั้ง 2 set
- ใน profile ระบุ:
  ```yaml
  business_type: "hybrid"
  hybrid_components: ["creator", "product"]   # หรืออื่นๆ ตาม mix
  primary_component: "creator"                # อันไหนหลัก — ใช้เป็น default behavior
  ```

### Default Behavior
- ใช้ `primary_component` เป็น default — เช่น primary=creator → เขียนแบบ creator + soft promo course เฉพาะ slot ที่ pillar=Promo
- Research ใช้ทั้ง strategies ของ component ที่อยู่ใน list
- CTA สลับ — บางโพสต์ใช้ creator-CTA, บางโพสต์ promo-CTA ตาม `monetization.promo_frequency`

---

## Decision Tree: เลือก type ยังไง

ถาม 3 คำถาม:

1. **คุณขายสินค้า/บริการตรงๆ ผ่านเพจไหม?**
   - ใช่ + ขายตลอด → `product`
   - ใช่ แต่ส่วนน้อย ส่วนใหญ่เป็นเนื้อหาให้ความรู้ → `hybrid` (primary: creator)
   - ไม่ → ไป 2

2. **คุณเป็นแบรนด์ของตัวคน หรือ แบรนด์เนื้อหา?**
   - แบรนด์ของตัวคน (รับงานในนามตัวเอง) → `personal_brand`
   - แบรนด์เนื้อหา (เพจเป็นหลัก คนตามเพจไม่ใช่คุณ) → `creator`
   - ทั้งคู่ → `hybrid` (primary: personal_brand)

3. **รายได้หลักมาจากอะไร?**
   - ขายสินค้า → product
   - ขาย service ให้ลูกค้าเฉพาะตัว → personal_brand
   - sponsor/ad/course/affiliate → creator
   - หลายทาง → hybrid

---

## Migration

ถ้าผู้ใช้มี profile แบบเดิม (v0.1) ที่ไม่มี `business_type` field — `business-profile-manager` ตรวจเจอ → ถามผู้ใช้ + เติม field ที่ขาด ไม่ทับ field ที่มี

หลังเพิ่ม `business_type`, skill อาจ suggest field ใหม่ที่ relevant กับ type นั้น (เช่น product → ถาม pain_points; creator → ถาม unique_perspective)
