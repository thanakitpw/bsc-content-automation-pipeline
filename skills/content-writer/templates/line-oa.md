# LINE OA Broadcast Template

## Structure

### Hook (1 บรรทัด)
- สั้นมาก ≤ 12 คำ
- LINE OA แสดง preview แค่ ~50 ตัวอักษร — ต้องเด็ดที่บรรทัดแรก

### Body (3-5 บรรทัด)
- 1 idea หลัก
- ห้ามยาวเกิน 100 คำ — LINE จะ truncate

### CTA + Button
- 1 button text สั้น (≤ 14 ตัวอักษร) เช่น "ดูสินค้า", "ทักแชท", "จองเลย"
- ใส่ link ที่จะเอาไปใส่ใน button (ถ้ามี)

## Length Target

LINE OA มี 500 char limit ต่อ message — เป้าจริงควร 200-350 char เพื่อให้คนอ่านจบ

## LINE-Specific Rules

- ✅ Emoji 2-3 ตัว — culture ของ LINE ชอบ emoji
- ✅ Break line ทุก 1-2 ประโยคอ่านง่ายในมือถือ
- ✅ ระบุชื่อแบรนด์ทุก message — คนอ่าน LINE OA หลายเพจ ต้องชัด
- ❌ ไม่ส่ง broadcast > 1 ครั้ง/วัน (ส่งเยอะคน mute)
- ❌ ไม่ใส่ URL ดิบ — ใส่ใน button เท่านั้น

## Output Format

เพราะ LINE OA platform ใส่ button ผ่าน UI เอง ไม่ใช่ markdown — output เขียนเป็น 2 ส่วน:

```markdown
## Message Body

<text ที่จะ paste ลง LINE OA>

## Button

- Text: <button label>
- URL: <link>
```
