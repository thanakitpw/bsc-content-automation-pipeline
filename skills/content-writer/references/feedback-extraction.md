# Feedback Extraction

วิธีดึง before/after + rule จากการแก้ของผู้ใช้

## เมื่อผู้ใช้แก้ draft แบบไหน

### Type A: ผู้ใช้พิมพ์ rewrite ที่ต้องการให้

เช่น:
> "เปลี่ยนย่อหน้าแรกเป็น: เคยมั้ย ใช้ครีมมา 5 ตัวยังไม่หาย?"

→ before = ย่อหน้าแรกเดิมจาก draft v1
→ after = ข้อความที่ผู้ใช้พิมพ์
→ rule = ต้องถามผู้ใช้ generalize

### Type B: ผู้ใช้บอก instruction

เช่น:
> "อย่าใช้คำว่า 'นะคะ' ลงท้ายทุกประโยค"

→ ไม่มี before/after ตรงๆ
→ rule = instruction ที่ผู้ใช้พิมพ์ — ใช้ตรงๆ
→ context = "user แจ้งระหว่างแก้ draft <slug>"

### Type C: ผู้ใช้บอก "ไม่ชอบ" โดยไม่ระบุ

เช่น:
> "ย่อหน้านี้น่าเบื่อ"

→ ถามต่อ — "อยากให้แก้เป็นแบบไหน?" หรือ "rule ที่อยากให้ apply คืออะไร?"
→ ห้าม guess แล้ว save style note โดย user ยังไม่ confirm

## ขั้นตอนการ extract

1. **identify diff**: หาส่วนที่ผู้ใช้แก้ — ถ้า user ไม่ชี้ ให้ถาม
2. **propose 2-3 generalized rules**: เสนอ rule ที่จะ generalize ได้ ใช้ AskUserQuestion ให้เลือก
   ตัวอย่าง — ถ้า user แก้ hook จาก "ขอเสนอครีม" เป็น "เคยมั้ย ใช้ครีมมา 5 ตัว..." เสนอ:
   - (a) "เปิด FB post ด้วย pain question ไม่ใช่ promo announcement"
   - (b) "ห้ามใช้คำว่า 'ขอเสนอ' เปิดบทความ"
   - (c) "Hook ต้องระบุจำนวนหรือ specific detail (เช่น '5 ตัว')"
3. **confirm before save**: แสดง full style note ที่จะ append → user confirm/edit/cancel
4. **call business-profile-manager**: trigger operation 5 เพื่อ append เข้า style-notes.md

## Quality Bar สำหรับ Rule

ดี:
- ✅ เป็น "do/don't" ที่ apply ได้กับบทความอื่น
- ✅ มี reasoning ชัด
- ✅ specific พอ — ไม่ใช่ "เขียนให้ดี"

ไม่ดี:
- ❌ rule ที่ใช้ได้แค่บทความเฉพาะ
- ❌ rule ขัดกับ profile.voice (ต้องเตือน user — อาจต้อง update profile แทน)
- ❌ rule ที่ user ยังไม่ confirm
