# Style Notes — ตัวอย่างที่ดี

ไฟล์นี้แสดงวิธีเขียน style note ที่มีประโยชน์ต่อ content-writer

## ตัวอย่าง 1: Rewrite Pattern

```markdown
## 2026-05-10 - Rewrite

**Context**: User แก้บทความเปิดร้านครีม เปลี่ยนวิธีเปิดเรื่อง

**Rule**: เปิดด้วย pain point เป็นคำถาม ไม่ใช่ประกาศโปร

**Before**:
> ขอเสนอครีมรุ่นใหม่ เพิ่งเปิดตัววันนี้! ลด 50%

**After**:
> เคยมั้ย — ใช้ครีมมา 5 ตัวแล้วสิวยังไม่หาย? วันนี้มีตัวที่ทีมพัฒนามา 2 ปี

**Rationale**: คนเลื่อนผ่านโปรเร็ว แต่หยุดดูถ้าตรงกับปัญหาตัวเอง
```

**ทำไมดี**: มี before/after ชัดเจน + ระบุ rule ที่ generalize ได้ + อธิบายเหตุผล

---

## ตัวอย่าง 2: Rule Statement (ไม่มี before/after)

```markdown
## 2026-05-10 - Rule

**Context**: User แจ้งว่าเพจไม่ใช้คำลงท้าย "นะคะ" เพราะ tone อยากเป็น expert ไม่ใช่ sales

**Rule**: ห้ามลงท้ายประโยคด้วย "นะคะ", "นะจ๊ะ", "จ้า" — ใช้ "ครับ/ค่ะ" เท่านั้น และไม่ทุกประโยค

**Rationale**: เพจ position เป็น authority ไม่ใช่ peer
```

**ทำไมดี**: rule กว้างพอที่จะใช้ได้ทุกบทความ + อธิบายเหตุผลเชิงกลยุทธ์ ไม่ใช่แค่ "ไม่ชอบ"

---

## ตัวอย่าง 3: Structural Pattern

```markdown
## 2026-05-10 - Rule

**Context**: User ชอบโครงสร้างบทความ FB ที่ทดลองมา 3 อาทิตย์

**Rule**: บทความ FB ใช้โครง 4 ย่อหน้า:
1. Hook (1-2 บรรทัด คำถาม/สถิติ)
2. Pain elaboration (3-4 บรรทัด สะท้อนความรู้สึกคนอ่าน)
3. Solution + product mention (5-7 บรรทัด)
4. CTA + tag (1-2 บรรทัด)

ห้ามเขียนเกิน 4 ย่อหน้าใน FB post

**Rationale**: เกิน 4 ย่อหน้า engagement ตก 40% จากที่ทดสอบ
```

**ทำไมดี**: ระบุ structure ตรงๆ + มีข้อมูลสนับสนุน

---

## รูปแบบที่ "ไม่ดี"

### หลวม/กว้างเกินไป

```markdown
## 2026-05-10
ให้เขียนดีๆ
```
→ ปัญหา: writer ไม่รู้ "ดี" คืออะไร

### ระบุแค่ตัวอย่างไม่มี rule

```markdown
**Before**: ขอเสนอครีม
**After**: เคยมั้ย ใช้ครีม...
```
→ ปัญหา: ไม่ generalize ได้ — writer ไม่รู้ว่าจะ apply pattern นี้กับบทความอื่นยังไง

### Rule ขัดกับ rule อื่น

ถ้า rule ใหม่ขัดกับ rule เก่าใน Active Rules — skill ต้องเตือน user ก่อน save
ให้ user ตัดสินใจว่า:
- ทับ rule เก่า
- เก็บทั้งคู่ (มีเงื่อนไขใช้ต่างกัน — เพิ่มใน context)
- ยกเลิกการ save

---

## Promotion จาก History → Active Rules

เมื่อ rule เดียวกันถูก append ซ้ำ 3+ ครั้งจาก feedback ต่างเหตุการณ์ — skill เสนอให้ "promote" ขึ้น Active Rules section ที่ด้านบนของ style-notes.md เพื่อ:
1. ทำให้ writer มอง rule นั้นชัดขึ้น (อยู่ต้นไฟล์)
2. ลด clutter ใน history

ขอ confirm กับ user ก่อน promote
