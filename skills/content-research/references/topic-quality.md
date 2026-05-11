# Topic Quality Criteria

เกณฑ์ใช้คัด topic ที่ "ดี" สำหรับเสนอผู้ใช้ — ไม่ใช่แค่ "AI คิดได้"

## เกณฑ์หลัก 4 ข้อ

### 1. Source-Backed (มีแหล่ง)
- ✅ Pantip thread ที่มี > 30 replies
- ✅ Reddit post ที่มี upvote สูง
- ✅ Search trend จาก Google PAA
- ❌ "ฉันคิดว่าหัวข้อนี้น่าสนใจ"

### 2. Audience-Fit (ตรงกลุ่มเป้าหมาย)
- ✅ ตอบ pain point ใน profile.target_audience.pain_points
- ✅ เกี่ยวข้องกับ products[].target_pain
- ❌ topic กว้างที่ใครก็เขียนได้

### 3. Differentiated (ต่างจากคู่แข่ง)
- ✅ คู่แข่งยังไม่พูด หรือ พูดแต่จาก angle อื่น
- ✅ มี angle เฉพาะของแบรนด์ (เช่น sustainability, science-backed)
- ❌ ทำซ้ำที่คู่แข่งเพิ่งโพสต์เมื่อสัปดาห์ก่อน

### 4. Actionable (ผู้อ่านทำต่อได้)
- ✅ ลงท้ายด้วย step ที่ทำได้ทันที
- ✅ ชี้ไปยัง CTA ของแบรนด์ได้แบบไม่ฝืน
- ❌ "เรื่องน่ารู้" ที่จบลอยๆ ไม่นำไปสู่อะไร

## Search Intent Types

ใช้กำหนด angle และ structure:

### Information (รู้ข้อมูล)
- เช่น "วิธีล้างหน้าถูกต้อง"
- format: How-to, listicle, tutorial
- CTA: subscribe / follow

### Decision (ก่อนตัดสินใจซื้อ)
- เช่น "ครีม X กับ Y ต่างกันยังไง"
- format: Comparison, review, case study
- CTA: ลองสินค้า / ทักแชทถาม

### Entertainment (อ่านสนุก)
- เช่น "5 เรื่องตลกของพนักงานคลินิก"
- format: Story, list with humor
- CTA: comment / share

### Inspiration (แรงบันดาลใจ)
- เช่น "จากสิวเรื้อรัง 5 ปี → หน้าใส"
- format: Personal story, transformation
- CTA: เริ่มเส้นทางตัวเอง

## Anti-Patterns (หลีกเลี่ยง)

### Topic ที่กว้างเกิน
- ❌ "เคล็ดลับการตลาด"
- ❌ "ทำธุรกิจให้สำเร็จ"
- ✅ "วิธีตอบ inbox ลูกค้าครีมที่บ่นเรื่องสิว ให้เขาเชื่อใจ"

### Topic ที่ใช้ข้อมูลผิด
- ❌ "งานวิจัยล่าสุดบอกว่า..." โดยไม่มีแหล่ง
- ❌ "สถิติคนไทย 80% ใช้..." แล้วไม่อ้างอิง
- ✅ ถ้าจะใช้ stat ต้องมี source URL จากที่ค้นมาจริง

### Topic ที่ negative ต่อคู่แข่ง
- ❌ "ครีม X ไม่ดี อย่าซื้อ"
- ✅ "ครีมราคาไม่ถึง 500 ที่ตอบโจทย์สิวฮอร์โมน — เปรียบเทียบเทคโนโลยี"

### Topic ที่อ้างหรือสัญญาเกินจริง
- ❌ "หายขาด 100% ใน 7 วัน"
- ❌ "รับรองผล ไม่ได้ผลคืนเงิน"
- ✅ "วิธีเร่งฟื้นฟูผิวที่ทีมเรา recommend หลังลองมาแล้ว 30 เคส"

## Scoring (ใช้ตอน rank topics)

ถ้ามี topic ideas เกิน 4 ตัว ใช้ score คัด top 4 สำหรับ AskUserQuestion:

| เกณฑ์ | คะแนน |
|-------|------|
| มี source signal แข็ง (Pantip 100+ replies / cite-able stat) | +3 |
| ตรง pain ใน profile โดยตรง | +2 |
| Differentiated จากคู่แข่ง | +2 |
| Actionable + CTA fit | +1 |
| Search intent ชัด | +1 |

Topic ที่ได้ ≥ 5 คะแนนเข้ารอบ
